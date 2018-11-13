import org.springframework.web.bind.annotation.RequestBody;

import org.springframework.web.bind.annotation.RequestMapping;

import org.springframework.web.bind.annotation.RequestParam;

import org.springframework.web.bind.annotation.RestController;

import javax.annotation.Resource;

import java.util.List;

import java.util.Map;

import com.netflix.hystrix.contrib.javanica.annotation.HystrixCommand;

import com.google.common.collect.Lists;

import org.springframework.beans.BeanUtils;

import org.springframework.data.domain.Page;

import org.springframework.util.CollectionUtils;

@SpringBootApplication
@EntityScan(basePackages="com.hikvision.tms.open.entity")
@ComponentScan(basePackages = "com.hikvision.tms")
@EnableDiscoveryClient
@EnableScheduling
@EnableFeignClients(basePackages = "com.hikvision.tms")
@EnableCaching
@EnableAsync
@EnableWs
