## 10分钟运行一个shiro程序 来源于shiro官网

http://shiro.apache.org/tutorial.html

##### 1.随意创建一个新目录，shiro-tutorial并在将创建pom.xml文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
    <project xmlns="http://maven.apache.org/POM/4.0.0"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">

    <modelVersion>4.0.0</modelVersion>
    <groupId>org.apache.shiro.tutorials</groupId>
    <artifactId>shiro-tutorial</artifactId>
    <version>1.0.0-SNAPSHOT</version>
    <name>First Apache Shiro Application</name>
    <packaging>jar</packaging>

    <properties>
        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
    </properties>

    <build>
        <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>3.8.0</version>
                <configuration>
                    <source>1.6</source>
                    <target>1.6</target>
                    <encoding>${project.build.sourceEncoding}</encoding>
                </configuration>
            </plugin>

        <!-- This plugin is only to test run our little application.  It is not
             needed in most Shiro-enabled applications: -->
            <plugin>
                <groupId>org.codehaus.mojo</groupId>
                <artifactId>exec-maven-plugin</artifactId>
                <version>1.1</version>
                <executions>
                    <execution>
                        <goals>
                            <goal>java</goal>
                        </goals>
                    </execution>
                </executions>
                <configuration>
                    <classpathScope>test</classpathScope>
                    <mainClass>Tutorial</mainClass>
                </configuration>
            </plugin>
        </plugins>
    </build>

    <dependencies>
        <dependency>
            <groupId>org.apache.shiro</groupId>
            <artifactId>shiro-core</artifactId>
            <version>1.4.1</version>
        </dependency>
        <!-- Shiro uses SLF4J for logging.  We'll use the 'simple' binding
             in this example app.  See http://www.slf4j.org for more info. -->
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>slf4j-simple</artifactId>
            <version>1.7.21</version>
            <scope>test</scope>
        </dependency>
        <dependency>
            <groupId>org.slf4j</groupId>
            <artifactId>jcl-over-slf4j</artifactId>
            <version>1.7.21</version>
            <scope>test</scope>
        </dependency>
    </dependencies>

</project>
```

#### 2.创建项目的基本目录

创建一个 `src/main/java`子目录。在`src/main/java`创建`Tutorial.java`

```java
import org.apache.shiro.SecurityUtils;
import org.apache.shiro.authc.*;
import org.apache.shiro.config.IniSecurityManagerFactory;
import org.apache.shiro.mgt.SecurityManager;
import org.apache.shiro.session.Session;
import org.apache.shiro.subject.Subject;
import org.apache.shiro.util.Factory;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Tutorial {

    private static final transient Logger log = LoggerFactory.getLogger(Tutorial.class);

    public static void main(String[] args) {
        log.info("我的第一个shiro程序");
        System.exit(0);
    }
}
```

#### 3.测试运行

在项目根目录下 命令后中输入

```bash
mvn compile exec:java
```

等下载好依赖就可以看到命令行打出"我的第一个shiro程序"啦！！这时候说明没啥出错，可以正式进去shiro世界

#### 4.启动shiro

在应用程序中启用Shiro时要了解的第一件事是，Shiro中的几乎所有内容都与称为的中央/核心组件有关`SecurityManager`。(我擦勒，这不就跟springmvc的DispatcherServlet差不多嘛)

我们将使用INI文件`SecurityManager`为该简单应用程序配置Shiro 。首先，创建一个**`src/main/resources`**目录，然后`shiro.ini`在该新目录中创建一个包含以下内容的文件：

```ini
# =============================================================================
# Tutorial INI configuration
#
# Usernames/passwords are based on the classic Mel Brooks' film "Spaceballs" :)
# =============================================================================

# -----------------------------------------------------------------------------
# Users and their (optional) assigned roles
# 用户和他的角色
# 用户名 = 密码, role1, role2, ..., roleN
# -----------------------------------------------------------------------------
[users]
root = secret, admin
guest = guest, guest
presidentskroob = 12345, president
darkhelmet = ludicrousspeed, darklord, schwartz
lonestarr = vespa, goodguy, schwartz

# -----------------------------------------------------------------------------
# Roles with assigned permissions
# 角色和他所拥有的权限
#角色名=权限1，权限2
# roleName = perm1, perm2, ..., permN
# -----------------------------------------------------------------------------
[roles]
admin = *
schwartz = lightsaber:*
goodguy = winnebago:drive:eagle5
```

此配置基本上设置了一小组静态用户帐户，足以满足我们第一个应用程序的需要

#### 5.引入配置启动一下shiro

```java
public static void main(String[] args) {

    log.info("My First Apache Shiro Application");

    //1.
    Factory<SecurityManager> factory = new IniSecurityManagerFactory("classpath:shiro.ini");

    //2.
    SecurityManager securityManager = factory.getInstance();

    //3.
    SecurityUtils.setSecurityManager(securityManager);

    System.exit(0);
}
```

老规矩命令行敲

 ```
mvn compile exec:java
 ```

#### 6.使用shiro

shiro最重要的就是Subject，代表着当前用户，其实就是user嘛 换了个命名而已

在几乎所有环境中，您都可以通过以下调用获取当前执行的用户：

```
Subject currentUser = SecurityUtils.getSubject();
```

现在有了`Subject`，不就可以随意进行各种操作了么

```
Session session = currentUser.getSession();
session.setAttribute( "someKey", "aValue" );
```

这`Session`是Shiro特有的实例，它提供了常规HttpSession所使用的大部分功能，但有一些额外的好处和一个**很大的**不同：它不需要HTTP环境！

直接贴出代码，解释注释里面都有噢 不难理解

```java
import org.apache.shiro.SecurityUtils;
import org.apache.shiro.authc.*;
import org.apache.shiro.config.IniSecurityManagerFactory;
import org.apache.shiro.mgt.SecurityManager;
import org.apache.shiro.session.Session;
import org.apache.shiro.subject.Subject;
import org.apache.shiro.util.Factory;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

public class Tutorial {

    private static final transient Logger log = LoggerFactory.getLogger(Tutorial.class);

    public static void main(String[] args) {
        log.info("My First Apache Shiro Application");

        Factory<SecurityManager> factory = new IniSecurityManagerFactory("classpath:shiro.ini");
        SecurityManager securityManager = factory.getInstance();
        SecurityUtils.setSecurityManager(securityManager);

        // 获取当前正在执行的subject，不管有无登陆都可获取
        Subject currentUser = SecurityUtils.getSubject();

        // 获取shiro自身自带的session 功能与httpsession(no need for a web or EJB container!!!)
        Session session = currentUser.getSession();
        session.setAttribute("someKey", "aValue");
        String value = (String) session.getAttribute("someKey");
        if (value.equals("aValue")) {
            log.info("Retrieved the correct value! [" + value + "]");
        }

        // let's login the current user so we can check against roles and permissions:
      //登陆并且检查角色与权限
        if (!currentUser.isAuthenticated()) {
            UsernamePasswordToken token = new UsernamePasswordToken("lonestarr", "vespa");
            token.setRememberMe(true);
            try {
                currentUser.login(token);
            } catch (UnknownAccountException uae) {
                log.info("There is no user with username of " + token.getPrincipal());
            } catch (IncorrectCredentialsException ice) {
                log.info("Password for account " + token.getPrincipal() + " was incorrect!");
            } catch (LockedAccountException lae) {
                log.info("The account for username " + token.getPrincipal() + " is locked.  " +
                        "Please contact your administrator to unlock it.");
            }
            // ... catch more exceptions here (maybe custom ones specific to your application?
            catch (AuthenticationException ae) {
                //unexpected condition?  error?
            }
        }

        //say who they are:
        //print their identifying principal (in this case, a username):
        log.info("User [" + currentUser.getPrincipal() + "] logged in successfully.");

        //test a role:
        if (currentUser.hasRole("schwartz")) {
            log.info("May the Schwartz be with you!");
        } else {
            log.info("Hello, mere mortal.");
        }

        //test a typed permission (not instance-level)
        if (currentUser.isPermitted("lightsaber:wield")) {
            log.info("You may use a lightsaber ring.  Use it wisely.");
        } else {
            log.info("Sorry, lightsaber rings are for schwartz masters only.");
        }

        //a (very powerful) Instance Level permission:
        if (currentUser.isPermitted("winnebago:drive:eagle5")) {
            log.info("You are permitted to 'drive' the winnebago with license plate (id) 'eagle5'.  " +
                    "Here are the keys - have fun!");
        } else {
            log.info("Sorry, you aren't allowed to drive the 'eagle5' winnebago!");
        }

        //all done - log out!
        currentUser.logout();

        System.exit(0);
    }
}
```

上面就是shiro的基本用法啦～～～ 还挺简单的。

