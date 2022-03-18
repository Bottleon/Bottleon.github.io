---
layout: single
title: "Spring에 관하여"
categories: framework
permalink: spring/chapter01
toc: true
author_profile: true
sidebar_main: true
---

# Spring이란?

## Spring정의

웹어플리케이션을 만들기 위한 자바기반 스프링프레임워크입니다.

## Spring의 특징

1. 자바 객체와 라이브러리들을 관리해주고 톰캣과 같은 WAS가 내장되어 있습니다.
2. 자바 객체를 Spring내부에서 생명주기를 관리하고 필요한 객체는 Spring Container에서 가져와서 사용합니다.
3. IOC와 DI

```
DI : 'Dependency Injection'로 "의존성 주입"이라는 의미
로 객체를 직접 생성하는 것이 아니라 외부에서 생성한 후 주입
시켜주는 방식입니다. 이것은 웹서버를 킬 때 bean으로 정의된
객체들이 스프링에서의 서블릿디스페치를 통해 init메서드가
실행되는데 여기서 서블릿컨테이너에 등록되고 실행이 완료된 후
어떠한 객체를 부르는데 해당 객체에서 다른 객체를 사용해야 될
경우 setter를 서블릿컨테이너가 실행 해줌으로 의존성이 주입됩니다.
의존성 주입을 해야되는 객체들은 싱글톤으로 이루어져있습니다.

public class a{
    private B b;
    public void setB(B b){
        this.b = b;
    }
}

이런식으로 선언해놓으면 스프링컨테이너가 주입을 해줍니다.

IOC : 'Inversion of control'로 "제어의 역전"이라는 의미로
보통 객체에 대한 제어는 개발자가 하게 되는데 스프링은 스프링컨테이너가
xml에 있는 bean으로 정의된 객체를 읽고 객체를 제어해주게 됨으로써
제어의 역전이 된 것입니다.
```

4. ORM사용
   - JPA를 사용하여 객체에 데이터베이스에 대한 스키마를 정의해주면 자동으로 메핑시키고 respository를 이용하여 쿼리문과 쿼리 실행까지 가능하게 해줍니다.
5. maven을 사용하여 pom.xml에 dependency를 관리하게 됩니다.
   - spring boot에 비해 직접 넣고 install해줘야 되는게 번거롭습니다.
6. mvc패턴을 이용
   - mvc는 model,view,controller로 model에서는 서비스로직을 구현,
     view에서는 클라이언트의 요청을 controller로 전달하여 controller에서의 값을
     응답해주고 controller는 url요청을 처리해줍니다. 보통 모델에서는
     serviceFacade(비지니스로직구현+트렌잭션 관리),DAO 혹은 Mapper(데이터베이스 로직과 쿼리)로 이루어져 있습니다.
7. AOP를 사용
   - 공통관심사 분리를 하여 모듈화하게 해주는 기법입니다. 보통 logger,transaction,exception처리등을 AOP에 정의해줍니다.

## Spring의 동작원리

보통 톰캣이 켜지면 servlet의 객체들이 메모리에 등록되게 되고 DispathcerServlet에서
HTTPServelt을 상속받아 init메서드를 실행시키게 됩니다. init메서드에서는 스프링컨테이너가 등록되게 됩니다. 스프링 컨테이너에는 ApplicationContext(BeanFactor 상속)에서 BeanFactory의 객체 생성과 관리를 하며 트렌잭션도 관리를 해주고 bean에 등록된 클래스를 객체화시켜줍니다. BeanFactory에서는 스프링 설정파일에 등록된 객체를 생성 및 관리를 해주고 클라이언트의 요청에 따라 객체를 생성해줍니다.
또한 init메서드에서 handlerMapping을 통해 url.property파일에 url과 controller의 메핑 혹은 어노테이션으로 controller와 url의 메핑을 등록해줍니다.
클라이언트에서 요청이 들어오면 DispatcherServlet에서 doGet메서드를 실행하여 doPost메서드에 request와 response를 전달해주고(보안에 용이) doPost메서드에서 인코딩설정과 controller에 해당 request와 response를 전달해주고 ModelAndView를 통해 controller에서 처리된 결과와 view의 경로 혹은 view정보를 담은 객체를 받아와서
internalResourceviewResolver를 통해 해당 view단으로 이동시켜줍니다.
