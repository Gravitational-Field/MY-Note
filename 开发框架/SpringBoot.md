### Spring注解汇总

- @Autowired
- @Qualifier
- @Resource
- @Service、@Componment、@Repository、@Controller 用于向Spring容器中注册pojo
- @Bean  加在方法上，该方法会生产一个对象，并注册到Spring容器中


- @PathVariable("id")    用来获取URI参数中传过来的参数，来绑定到形参上

@RequestMapping   指定映射关系，哪种请求用该方法进行处理

@ResponseBody   被它修饰的controller类、方法会返回json类型数据

@RequestParam(value\="id", required\=true)int idnum  从request里获取值，而不是从uri中

- @Transactional  开启事务
- @Configuration




### SpringBoot注解汇总

- @SpringBootApplication

- @Mapper  用在Dao上，
- @RestController("/demo")
- @ControllerAdvice 
- @ExceptionHandler(Exception.class)
- @CookieValue
- @ReuqestParam