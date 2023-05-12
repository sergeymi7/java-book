# JWT

**JWT (JSON Web Token)** - это формат токенов, который используется для передачи информации между двумя сторонами в
удобном и безопасном формате. Он состоит из трех частей: заголовок (**header**), полезная нагрузка (**payload**) и
подпись (**signature**).

* Заголовок содержит информацию о типе токена и используемом алгоритме шифрования.
* Полезная нагрузка содержит информацию, которую мы хотим передать, например, идентификатор пользователя или время жизни
  токена.
* Подпись используется для проверки целостности токена.

**JWT** используется для аутентификации и авторизации в веб-приложениях и микросервисах. Когда пользователь успешно
аутентифицирован, ему выдается **JWT**, который он может использовать для доступа к защищенным ресурсам. При запросе
защищенного ресурса, **JWT** должен быть включен в заголовок запроса. Сервер может проверить подпись токена и получить
доступ к полезной нагрузке, чтобы убедиться, что пользователь имеет права на доступ к ресурсу.

**JWT** имеет несколько преимуществ по сравнению с традиционной сессионной аутентификацией:

1. Токены **JWT** хранятся на клиентской стороне, что уменьшает нагрузку на сервер и позволяет легко масштабировать
   приложение.
2. **JWT** не требует хранения информации о сессии на сервере, что упрощает процесс управления состоянием.
3. **JWT** может быть использован для аутентификации и авторизации в разных приложениях и микросервисах, не требуя общей
   базы данных сессий.

В **Java** для работы с **JWT** существует несколько библиотек, например, **jjwt** или **nimbus-jose-jwt**. Они
позволяют создавать и проверять **JWT**, а также работать с различными алгоритмами шифрования.

### Пример

```java
import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;

import java.util.Date;

public class JwtExample {

    private static final String SECRET_KEY = "mySecretKey"; // Замените на свой секретный ключ

    public static void main(String[] args) {
        String token = createToken("myUsername", 3600); // Создаем токен, который истекает через 1 час
        System.out.println(token);

        Claims claims = verifyToken(token); // Верифицируем токен и получаем его содержимое
        System.out.println(claims.getSubject()); // Выводим имя пользователя из содержимого токена
    }

    public static String createToken(String username, int expirationTimeInSeconds) {
        Date now = new Date();
        Date expirationDate = new Date(now.getTime() + expirationTimeInSeconds * 1000);

        return Jwts.builder()
            .setSubject(username)
            .setIssuedAt(now)
            .setExpiration(expirationDate)
            .signWith(SignatureAlgorithm.HS256, SECRET_KEY)
            .compact();
    }

    public static Claims verifyToken(String token) {
        return Jwts.parser()
            .setSigningKey(SECRET_KEY)
            .parseClaimsJws(token)
            .getBody();
    }
}
```

В этом примере создается **JWT** токен с именем пользователя и временем истечения срока действия токена. Для подписи токена
используется секретный ключ, который необходимо хранить в безопасности.

Затем токен верифицируется и извлекается его содержимое (здесь - имя пользователя).

В реальном приложении необходимо обеспечить безопасное хранение секретного ключа и реализовать проверку токена при
каждом запросе, который требует аутентификации.