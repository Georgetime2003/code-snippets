#### Exemple de patró Singleton per connexió a una BD MySQL
El patró Singleton és un patró de disseny encarregat de restringir la creció d'una sola instància d'una classe per poder reaprofitar-la

En aquest cas és un exemple per la creació d'una connexió a un sistema gestor de base de dades MySQL

```java
import java.sql.*;

public class DBMySQLManager {

    // Propietats
    private static Connection conn = null;
    private String driver = "com.mysql.cj.jdbc.Driver"; //com.mysql.jdbc.Driver
    private String url;
    private String usuari ="USUARI";
    private String contrasenya = "PARAULA DE PAS";
    private String host = "IP / HOST";
    private String base_dades = "NOM BASE DE DADES";

    // Constructors
    private DBMySQLManager(){

        this.url = "jdbc:mysql://" + host + ":3306/" + base_dades;

        try{
            Class.forName(driver);
            conn = DriverManager.getConnection(url, usuari, contrasenya);
        }
        catch(ClassNotFoundException | SQLException e){
            e.printStackTrace();
        }
    }

    // Mètodes
    public static Connection getConnection() {

        if (conn == null){
            new DBMySQLManager();
        }

        return conn;
    }
  
    public static closeConnection() {
        if (conn != null) {
          conn.close();
        }
    }
}
```
