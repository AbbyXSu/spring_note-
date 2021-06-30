# Spring_Note
inversion of Control 
- Container maintains your class dependencies
- IoC provides mechanism of dependency injection
-ApplicationContxts wraps the BeanFactory, which serves the beans to the runtime of the application 
- Spring Boots provides auto_ configuration of the ApplicationContexts
- objects injected at runtime or startup time 
- an object accepts the dependencies for construction instead of constrcuting them 
- if your class cannot operate without the dependency, it should be injected via constructors. 
- If your class can treat the dependency as optional or can accept multiple but variable concrete instances of the dependency, 
then it can be injected via setter injection. 

IoC Container manages every object in all classes to the main, 
IoC container handles injection via constructor argument at object creation for main.(We only configure these classes once no matter how many times that dependency is used and once we create it, 
we don't have to worry about it again)

Benefits of Dependency injection
- reduces noise in your code 
- reduces object coupling 
- reduces defects that arise from incorrect construction
- Focus on the API contract

Application Context 
Pupose of th application Context 
- Act as heart of Spring Application 
- Encapsulate the BeanFactory 
- Provides mechanism/metadata for bean creation 

Iversion of Control 
- provides all facilities for injection of beans at startup and runtime 
- Most of utiiliszing spring is actually configuring the IoC container 
_ BeanFactory handles all singlton beans

multiple ApplicationContests
- A spring applciation can have one or more ApplicationContxts objects in scope
- Web container always have multiple 
- Parents context can interact with children, not the other way around

Java_Based configure
Major Benefits of Java Configuration 
- Native language syntax 
- Compile time checking of configuration 
- Easier IDE integration 


Spring supports Maven and Gradle ( manage dependency)
- Spring Franework for providing comprehensive infrastrucual support for developing java appplication
- provides the plumbing
- OOP best pratice built in 
- Dont repeat yourself principle 

Some definitions 
- POJO - plain old java object 
- JavaBeans - simple object with only getters and setters 
- Springbeans _ POJOs configured in the application context 
- DTO _ Bean used to move state between layers 

inversion of Control 
- Container maintains your class dependencies
- IoC provides mechanism of dependency injection
-ApplicationContxts wraps the BeanFactory, which serves the beans to the runtime of the application 
- Spring Boots provides auto_ configuration of the ApplicationContexts

Why use Spring boot?
- Support rapid development 
- removes biolerplate of application setup 
- Many uses 
- cloud native support, but also traditional 


Spring Data
 - provides a common set of interfaces
 - Provides a common naming convention 
 - Provides aspected behavior 
 - Provides repository and data mapping convention
 - Remove boilerplate code
 - makes swapping data sources Easier
 - allows you to focus on business logic

 Key Components
- Repository interface
- pom.xml
- application.properties(connect with remote database instances)


> src > main > java/kotlin >com.xxxx.springframwork > data >entity > Guest

import javax.presistence.Id;
import javax.persistence.Table;
import java.sql.Date;

@Entity
@Table (name="Guest")
public class Guest {
    @Id 
    @Column(name="Guest_ID")
    @GeneratedValue (strategy = GenerationType.auto)
    private long guestId:
    @column(name="firstname")
    private String firstName;
    @column (name="last name")
    private string lastName;

// generate getter and setter 
    public long getGuestId(){
        return guestId;
    }

    public void setGuestId( long guestId){
        this.guestId = guestId;
    }
}


> src > main > java/kotlin >com.xxxx.springframwork > data > repository > GuestRepositry

import com.xxxxx.lil.learningspring.data.entity.guest
import org.springframwork.data.repository.crudRepository
import org.springframework. stereotype.repository

@Repository
public interface GuestRepository extends crudRepository<Guest,long>{

}


Dependency Injection Framework 
- allows you to focus on contracts 
- Develop business code only, leave construction to the container
- Build intermediate abstractions 

How ?
- IoC container is configured by developer 
- spring maintains handles to objects constructed at startup
- Spring serve singletons to classes during construction 
- Spring maintains lifecycle of beans
- developer only configures ApplicationContexts

> src > main > java/kotlin >com.xxxx.springframwork > business > service > Roomreservation

import com.xxxx.lil.learning spring.business.domain.Roomreservation;
import com.xxxxx.lil.learningspring.data.repository.GuestRepsoitory;
import com.xxxxx.lil.learningspring.data.repository.ReservationRepsoitory;
import com.xxxxx.lil.learningspring.data.repository.RoomRepsoitory;
import org.springframwork.stereotype.service
import org.springframwork.beans.factory.annotation.autowired

@service
public class ReservationService{
    private final RoomRepository roomRepository;
    private final GuestRepository guestRepository;
    private final ReservationRepsoitory reservationRepository;

    @autowired
    public reservationService(RoomRepository roomRepository,GuestRepository guestRepository,ReservationRepsoitory reservationRepository)
    this. roomRepository = roomRepository;
    this. guestRepository = guestRepository;
    this. reservationRepository = reservationRepository;
}

public List <Roomreservation> getRoomReservationsForDate(Date date){
    Iterable<Room> rooms = this.roomRepository.findAll();
    Map<long, Roomreservation> roomReservationMap = new HashMap();
    rooms.forEach(room ->{
        Roomreservation roomReservation = new Roomreservation();
        // populate tge room reservation
        roomReservation.setRoomId(room.getRoomId());
        roomReservation.setRoomName(room.getRoomName());
        roomReservation.setRoomnumber(room.getRoomNumber());
        roomReservationMap.put(room.getRoomId(),roomReservation);
    });
    Iterable<Resevation> reservations = this.reservationRepository.findReservationbyReservationDate(new java.sql.Date)
    reservations.forEach(reservation ->{
        RoomReservation roomReservation = roomReservationMap.get (reservation.getroomId());
        roomreservation.setDate(date);
        Guest guest = this.guestRepository.findById(reservation.getGuestId()).get();
        roomReservation.setFirstName(guest.getFirstName());
        roomReservation.setLastName(guest.getLastName());
        roomReservation.setGuestId(guest.getGuestId());
    });
    List <RoomResevation> roomReservations = new ArrayList<>();
    for(Long id: roomReservationMap.keyset()){
        roomReservation.add(roomReservationMap.get(id));
    }
    return roomReservation;
}


Model View Controller _ MVC
- Fundamental pattern for web application development
- Model is the data 
- view is the visual display thay is populated 
- controller wires the view with the Model

Spring Controller 

- Spring bean 
- annoted for the servlet mapping 
- Responds to incoming web requests 
- Outputs a view or raw data 

Template Engines 
- Spring support several template engines 
- Thymeleaf - most popular 
- Provides a DSL for HTML, leaving raw HTML documents
- Placeholders for dynamic data 
- Rendering engine allows for final product 


Build a Controller 

package com.frankmoley.lil.learningspring.web;

import java.text.Dataformat;
import java.text.simpleDateFormat;

public class dateUtils {
    privare static final dateFormat Date_Format = new SimpleDateFormat("yyyy-mm-dd");

    public static Date createDateFromDateString (String dateString)
        date date = null;
        if (null != dateString){
            try{
                date = Date_Format.parse(dateString);
            }catch (ParseException pe){
                date = new Date();
            }
        }else{
            date = new Date()
        }
        return date;
    }
}

package com.frankmoly.lil.learningspring.web

import org.springframwork.stereotype.Controller;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
@RequestMapping("/reeservations")
public class RoomReservationWebController {
    private final ReservationService reservationService;

    @autowired
    public RoomReservationWebController(ReservationService reservationService){
        this.reservationService = reservationService;
    }

    @GetMapping()
    public String getRoomReservations(value ="date", required = false)String datesTring,Model){
        Date date = DateUtils.createDateFromDateString(dateString);
        List <RoomReservation> roomReservation = this.reservationService.getRoomReservationsForDate(date);
        model.addAttribute("roomReservation",roomReservations);
        return "reservation";

    }
} 

Thymeleaf Views 
revservations.HTML

<!DOCTYPE html>
<html lanf ="en' xalns: th="http://www.Thymeleaf.org">
<head>
    <meta charset="UTF-8">
    <title>landon hotel : room reservations</title>
</head>
<body>
<h1>
<table>
    <tr>
        <td>room</td>
    </tr>
    <tr th:each="${roomReservation}
</html>

MockMVC

import Runwith 

@Runwith ( springJunit4ClassRunner.class)
@webMvcTest(RoomReservationWebController.class)
publc class RoomReservationWebController{
    @MockBean
    pivate ReservationService reservationService;

    @autowired
    privare MockMvc mockMvc;

    @Test 
    public voi getReservations() throws  Exception{
        String datastring ="2020-01-01";
        Data date = DateUtils.createDateFromDateString(dateString);
        List<RoomReservation> roomReservation = new ArrayList<>();
        RoomReservation roomReservation = new RoomReservation();
        roomReservation.setLastName("unit");
        roomReservation.setFirstName("Junit");
        roomReservation.setDate(date);
        roomReservation.setGuestId(1);
        roomReservation.add(roomReservation);
        given (reservationService.getRoomReservationsForDate(date)).willReturn(roomReservation)
                
        this.mockMvc.perform(get("/reservations?date=2020-02-02".andExpect(status(.isok()).andExpect(contect().string(containsString("unit,Junit")));
    }
}

RestController 
- Spring uses controllers for RESTful web services 
- just another MVC,only our view is JSON
- Once you understand the paradigm, its straight forward 
_spring marshals Json for you
- You can configure XML if desired 


@RestController
@RequesrMapping("api/reservations")
public class RoomReservationWebServicesController{
    privare final ReservationService reservationService;

    @Autowired 
    pubic RoomReservationWebController(ReservationService reservationService){
        this.reservationService = reservationService;
    }

    @GetMapping 
    public List <RoomReservation> getRoomReservations(@RequesrParam(name="date", required = false)String){
        Date date = DateUnils.createDateFromDateString(dateString);
        return this.reservationService.getRoomReservationsForDate(date);
    }
}
