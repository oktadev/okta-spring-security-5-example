# Spring Security 5 + Okta
 
An example app that shows how to use OIDC with Spring Security 5 and Okta. 

Please read [Get Started with Spring Security 5.0 and OIDC](https://developer.okta.com/blog/2017/12/18/spring-security-5-oidc) to see how this app was created.

**Prerequisites:** [Java 8](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html).

> [Okta](https://developer.okta.com/) has Authentication and User Management APIs that reduce development time with instant-on, scalable user infrastructure. Okta's intuitive API and expert support make it easy for developers to authenticate, manage, and secure users and roles in any application.

* [Getting Started](#getting-started)
* [Links](#links)
* [Help](#help)
* [License](#license)

## Getting Started

To install this example application, run the following commands:

```bash
git clone https://github.com/oktadeveloper/okta-spring-security-5-example.git
cd okta-spring-security-5-example
```

This will get a copy of the project installed locally. To install all of its dependencies and start the app, run:
 
```bash
./mvnw spring-boot:run
```

### Create an Application in Okta

You will need to [create an OpenID Connect Application in Okta](https://developer.okta.com/blog/2017/12/18/spring-security-5-oidc#create-an-openid-connect-app) to get your values to perform authentication. 

Log in to your Okta Developer account (or [sign up](https://developer.okta.com/signup/) if you don’t have an account) and navigate to **Applications** > **Add Application**. Click **Web**, click **Next**, and give the app a name you’ll remember. Click **Done** and copy the `clientId` and `clientSecret` into `server/src/main/resources/application.yml`. 

```yaml
spring:
  thymeleaf:
    cache: false
  security:
    oauth2:
      client:
        registration:
          okta:
            client-id: {clientId}
            client-secret: {clientSecret}
        provider:
          okta:
            authorization-uri: https://{yourOktaDomain}.com/oauth2/default/v1/authorize
            token-uri: https://{yourOktaDomain}.com/oauth2/default/v1/token
            user-info-uri: https://{yourOktaDomain}.com/oauth2/default/v1/userinfo
            jwk-set-uri: https://{yourOktaDomain}.com/oauth2/default/v1/keys
```

**NOTE:** The value of `{yourOktaDomain}` should be something like `dev-123456.oktapreview`. Make sure you don't include `-admin` in the value!

After modifying this file, restart your app and you'll be prompted to click on an "Okta" link to log in.

## Links

This example uses Spring Security's [OAuth 2.0 Login](https://docs.spring.io/spring-security/site/docs/5.0.0.RELEASE/reference/htmlsingle/#jc-oauth2login) feature.

## Help

Please post any questions as comments on the [blog post](https://developer.okta.com/blog/2017/12/18/spring-security-5-oidc), or visit our [Okta Developer Forums](https://devforum.okta.com/). You can also email developers@okta.com if you would like to create a support ticket.

## License

Apache 2.0, see [LICENSE](LICENSE).
