# TP1-JDBC
Test jdbc

Voici les etapes pour pouvoir utiliser une base de donnee a l'aide d'un code java:
On installe MySQL Workbench et le connector/J version 8.0.32.
Ensuite on telecharge le fichier mysql-connector-j-8.0.32. 
On va ensuite sur intelliJ: version IntelliJ IDEA Community Edition 2022.2.1.

On cree un nouveau projet, maintenant il faut connecter notre projet a la bade de donnee:
File -> Project Structure -> module -> add jar file puis on selectionne le fichier mysql-connector que l'on vient de telecharger.

import a faire:
import java.sql.DriverManager;
import java.sql.Statement;
import java.sql.Connection;
import java.sql.ResultSet;

Dans notre main il faudra lancer la connection a l'aide des commandes:
Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/nom_de_la_BDD", "identifiant_DBB", "mot_de_passe_DBB");
Statement statement = connection.createStatement();

Maintenant on a acces a cette database, on peut effectuer la commande suivante pour tester le fonctionnement:
(Test effectue sur la table person cree au prealable sur MySQL)
ResultSet resultSet =statement.executeQuery("select * from person");

Code complet: 

import java.sql.DriverManager;
import java.sql.Statement;
import java.sql.Connection;
import java.sql.ResultSet;

public class MyJDBC {
    public static void main(String[] args) {

        try {
            Connection connection = DriverManager.getConnection("jdbc:mysql://localhost:3306/jdbc-test1", "root", "root");
            Statement statement = connection.createStatement();

            ResultSet resultSet =statement.executeQuery("select * from person");

            while (resultSet.next()) {
                System.out.println(resultSet.getString("firstName"));
            }
        } catch( Exception e){
            e.printStackTrace();
        }
    }
}
