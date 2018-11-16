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
@Query(value = "update TMS_SYSTEM_ANNOUNCEMENTS t set t.data_status = 1 where t.id = ? and t.line_status = 1",
nativeQuery = true)
@Modifying
@Transactional

import javax.xml.bind.annotation.XmlAccessType;
import javax.xml.bind.annotation.XmlAccessorType;
import javax.xml.bind.annotation.XmlElement;
import javax.xml.bind.annotation.XmlType;

@ManyToOne(cascade={CascadeType.MERGE,CascadeType.REFRESH},optional=false)
    @JoinColumn(name="JOB_ID")
@RunWith(SpringJUnit4ClassRunner.class)
@SpringBootTest
Modifier.isStatic(field.getModifiers())
