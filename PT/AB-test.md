## Criando api de AB teste em 2 horas

### O que são testes AB

Resumidamente testes AB são aqueles que, um usuário siga um fluxo, e sempre siga esse fluxo, e algum outro siga o fluxo em 
uma mesma versão. Hoje em dia a gente usa testes AB para diversas coisas como: 

 - [x] Dividir fluxo de usuários (Ex: 10% irão assistir o botão na cor verde o resto de outra cor)
        _Detalhe importante nesse caso um usuário 'X' sempre deve ir para o mesmo fluxo_
        
 - [x] Rollout de features. Utilizado quando criar uma nova funcionalidade e quer ver como os usuários se comportam com ela,
 ou se vai ter algum problema de qualquer tipo, bug, performance, engajamento, na nova funcionalidade.
 
 Mas nada disso vai gerar o resultado que você espera caso não tenha como coletar os dados, então é importante saber qual 
 usuário seguiu e qual não seguiu e ver o resultado de qual resultado. Para isso já tivemos algumas abordagens para coleção,
 a mais simples delas é a própria aplicação dispara um log e se usar Kibana pode criar um dashboard para ver os resultados,
 qual lado foi melhor.
 
 Os testes AB são amplamente utilizados para ver qual alternativa vai ser melhor pra negócio, mas no caso de um bug, que 
 pode ser identificado em um rollout, ele pode representar uma redução nos custos operacionais para empresa.
 
 
 ### Tecnologias utilizadas
 
 - SpringBoot
 - H2 com configuração de arquivos
 - Hibernate 
 - Spring Web
 - JPA
 
 Basicamente é isso que precisamos para ter acesso a tudo. Caso evolua um pouco um mecanismo de cache é bem importante, 
 outra coisa as vezes é um banco melhor mas não acho que é necessário pois o H2 consegue ir até para um s3 e a gente utilizar
 o de lá.
 
 ## O projeto 
 
 A única classe que a gente vai precisar persistir  é a `Feature.kt` nela vai ter toda a lógica que precisamos no nosso caso 
 ela ficou assim 
 
 ```kotlin
import javax.persistence.Entity
import javax.persistence.GeneratedValue
import javax.persistence.Id

@Entity
data class Feature(var name: String = "",
                   var description: String = "",
                   var percentage: Int = 0) {
    fun userAbleUseFeature(ucode: String): Boolean {
        var ucodeNumber = ucode.hashCode()
        var result = (777 * ucodeNumber * this.id) % 100
        return result < this.percentage
    }

    @Id
    @GeneratedValue
    var id: Long = 0
}
```

A função `.entity.Feature#userAbleUseFeature` faz a lógica de um usuário ficar dentro da feature ou não. O 777 é só uma
constante do sistema para variar, ela não é necessária, mas eu acho bom não ter como multiplicador apenas o ID da feature.
Além disto o método `.hashCode()` retorna um int para qualquer string que chegar.


Os testes dessa parte ficaram em:  `com.luizleiteoliveira.abtest.entity.FeatureTest`
e a parte dos testes caso o usuário está ou não dentro de uma feature podem ficar bem similares com  os seguintes:

```kotlin
    @Test
    fun `user not able to use feature`() {
        val feature = Feature(name = "name", description = "description", percentage = 10)
        feature.id = 10
        val user = User("ucode")
        Assertions.assertEquals(10,  feature.id) // 777 * 10 * 111111138 = 45115764 % 100 = 64
        val userAbleUseFeature = feature.userAbleUseFeature(user.ucode)
        Assertions.assertFalse(userAbleUseFeature)
    }

    @Test
    fun `user able to use feature increase the percentage`() {
        val feature = Feature(name = "name", description = "description", percentage = 65)
        feature.id = 10
        val user = User("ucode")
        Assertions.assertEquals(10,  feature.id) // 777 * 10 * 111111138 = 45115764 % 100 = 64
        val userAbleUseFeature = feature.userAbleUseFeature(user.ucode)
        Assertions.assertTrue(userAbleUseFeature)
    }

    @Test
    fun `user able to use feature`() {
        val feature = Feature(name = "name", description = "description", percentage = 21)
        feature.id = 10
        val user = User("L")
        Assertions.assertEquals(10,  feature.id) // 76 * 10 * 111111138 = 590520 % 100 = 20
        val userAbleUseFeature = feature.userAbleUseFeature(user.ucode)
        Assertions.assertTrue(userAbleUseFeature)
    }
```  

E para finalizar a ultima coisa que precisamos é de criar o controller para a Feature.

Essa foi a parte mais tranquila e ficou assim:

```kotlin
import com.luizleiteoliveira.abtest.FeatureRepository
import com.luizleiteoliveira.abtest.entity.Feature
import org.springframework.web.bind.annotation.*

@RestController
@RequestMapping("/features")
class FeatureController(private val featureRepository: FeatureRepository) {

    @GetMapping
    fun getFeatures(): List<Feature> {
        return featureRepository.findAll().toList()
    }

    @PostMapping
    fun createFeature(@RequestBody feature: Feature): Long {
        featureRepository.save(feature)
        return feature.id
    }

    @PutMapping
    fun updateFeature(@RequestBody feature: Feature): Long {
        featureRepository.save(feature)
        return feature.id
    }

    @GetMapping("/{featureId}")
    fun checkUserAbleToUseFeature(@RequestParam("ucode") ucode: String, @PathVariable featureId: Long): Boolean {
        val feature = featureRepository.findById(featureId).get()
        return feature.userAbleUseFeature(ucode)
    }
}
```

E a configuração foi feita dentro do `application.properties`

```properties
spring.h2.console.enabled=true
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=password
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.datasource.url=jdbc:h2:file:/tmp/demo
```

### Conclusão 

 