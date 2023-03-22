### CORS policy issue

#### To fix the CORS policy issue, you need to modify your Spring Boot API to allow cross-origin requests from your React application.

1. First, uncomment the @Bean annotation for the corsConfigurer method in your Application class:
````
@Bean
public WebMvcConfigurer corsConfigurer() {
    return new WebMvcConfigurer() {
        @Override
        public void addCorsMappings(CorsRegistry registry) {
            registry.addMapping("/**")
                .allowedMethods("*")
                .allowedOrigins("http://localhost:3000")
                .allowedHeaders("*");
        }
    };
}
````
2. Add the @CrossOrigin annotation to your HelloWorldController class and specify the origin of your React application:
````
@RestController
@CrossOrigin(origins = "http://localhost:3000")
public class HelloWorldController {
    // ...
}
````
3. Finally, update the axios request in your React application to include the withCredentials option and set it to true:
````
axios.get('http://localhost:8080/hello-world', { withCredentials: true })
````
This should allow your React application to make cross-origin requests to your Spring Boot API without encountering a CORS policy error.

* Note: Make sure to replace http://localhost:3000 with the URL of your React application.
