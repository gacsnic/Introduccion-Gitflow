# Git-Flow en accion.

Vamos a crear un proyecto llamado HW el cual proporciona la salida Hola Mundo, utilizando el prototipo de Maven.

```
mvn archetype:generate -DgroupId=ni.gacssoft -DartifactId=hw  -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false  - DskipTests

```

Iniciamos el control de versiones con git-flow.
```
git init
git flow init
```

Creáremos la primer rama feature feature/config.
```
git flow feature start feature/config
```

Agregaremos un archivo .gitignore creado desde https://www.gitignore.io, con el siguiente contenido.
```
# Created by https://www.gitignore.io/api/linux,maven
# Edit at https://www.gitignore.io/?templates=linux,maven

### Linux ###
*~

# temporary files which can be created if a process still has a handle open of a deleted file
.fuse_hidden*

# KDE directory preferences
.directory

# Linux trash folder which might appear on any partition or disk
.Trash-*

# .nfs files are created when an open file is removed but is still being accessed
.nfs*

### Maven ###
target/
pom.xml.tag
pom.xml.releaseBackup
pom.xml.versionsBackup
pom.xml.next
release.properties
dependency-reduced-pom.xml
buildNumber.properties
.mvn/timing.properties
.mvn/wrapper/maven-wrapper.jar

# End of https://www.gitignore.io/api/linux,maven

```
Agregamos el archivo .gitignore y creamos el commit.

```
git add .gitignore
git commit -m"Se agrega el archivo gitignore"
```
Modificamos el pom.mxl y nos quedara de la siguiente manera:

```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>ni.gacssoft</groupId>
  <artifactId>hw</artifactId>
  <packaging>jar</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>hw</name>
  <url>http://maven.apache.org</url>

	  <dependencies>
	    <dependency>
	      <groupId>junit</groupId>
	      <artifactId>junit</artifactId>
	      <version>3.8.1</version>
	      <scope>test</scope>
	    </dependency>
	  </dependencies>

	 <properties> 
	        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
	        <maven.compiler.source>10</maven.compiler.source>
	        <maven.compiler.target>10</maven.compiler.target>
	</properties> 
</project>

```
Agregamos el archivo pom.xml, creamos el commit y cerramos la rama feature/config.

```
git add pom.xml
git commit -m"Se actualiza pom.xml"
git flow feature finish feature/config
```
Creamos una  feature feature/hw donde agregaremos nuestras características principales de nuestro proyecto Hola Mundo.
```
git flow feature start feature/hw
```

Modificamos el fichero App.java del proyecto HW y nos quedara así:
```
package ni.gacssoft;

/**
 * Hello world!
 * @author gacs
 */
public class App 
{
    public static void main( String[] args )
    {
        System.out.println( "h0la mundo!" );
    }
}
```
Agregamos los cambios, creamos el commit y cerramos la rama feature/hw.

```
git add App.java
git commit -m"Se modifica la clase App.java Hello World! por Hola Mundo!"
git flow feature finish feature/hw
```

Procedemos enviar a producción la versión 1.0.0 de proyecto HW.
```
git flow release start release/hw1.0.0
```
Antes de enviar a producción corregimos hola mundo por Hola Mundo y nos quedara de la siguiente forma:
```
package ni.gacssoft;

/**
 * Hello world!
 * @author gacs
 */
public class App 
{
    public static void main( String[] args )
    {
        System.out.println( "H0la Mundo!" );
    }
}
```
Agregamos los cambios, creamos el commit correspondiente y enviamos a producción la versión 1.0.0 de HW
```
git add App.java
git commit -m"Se corrige la salida de hola mundo por Hola Mundo!"
git flow release finish release/hw1.0.0
```
Bueno ya tenemos nuestra primera versión de HW, pero resulta que tenemos un bug, digitamos H0la en ves de Hola, de lo cual procederemos hacer corrección en la rama hotfix.
```
git flow hotfix start hotfix/hw1.0.1
```
Hacemos la reparación correspondiente el cual nos quedara de la siguiente forma.
```
package ni.gacssoft;

/**
 * Hello world!
 * @author gacs
 */
public class App 
{
    public static void main( String[] args )
    {
        System.out.println( "Hola Mundo!" );
    }
}
```
Agregamos los cambios, creamos el commit correspondiente y enviamos a producion y a desarrollo la reparación de la versión 1.0.0 de HW
```
git add App.java
git commit -m"Se corrige bug de la versiona 1.0.0  H0la mundo por Hola Mundo!"
git flow hotfix finish hotfix/hw1.0.1
```
Finalizamos el proyecto lo entregamos pero nos solicitan que ademas del Hola Mundo nos presente la fecha. De lo cual crearemos una clase estática con el nombre Util.java para que nos devuelva el dia y la fecha en formato dd/mm/yy.
Creamos la rama feature/today
```
git flow feature start feature/today
```
Creamos la clase estática Util.java con el siguiente contenido:
```
package ni.gacssoft;

import java.util.Calendar;


public class Util 
{
    public static String getToday(){
  		Calendar now = Calendar.getInstance();
        String strToday;
    	String[] strDay = new String[]{
            "Domingo",
            "Lunes",
            "Martes",
            "Miercoles",
            "Jueves",
            "Viernes",
            "Sabado"},
            strMonth=new String[]{
                "Enero",
                "Febrero",
                "Marzo",
                "Abril",
                "Mayo",
                "Junio",
                "Julio",
                "Agosto",
                "Septiembre",
                "Octubre",
                "Noviembre",
                "Diciembre",
            };
    strToday=strDay[now.get(Calendar.DAY_OF_WEEK) - 1]+"  "+now.get(Calendar.DAY_OF_MONTH)+" de "+strMonth[now.get(Calendar.MONTH) ]+" del "+now.get(Calendar.YEAR);
    return strToday;
    }
}
```
Agregamos la clase y creamos el commit correspondiente
```
git add Util.java
git commit -m"Se crea la clase estatica Util.java para obtener la fecha actual"
```
Una ves que tenemos la clase Util para obtener la fecha actual procederemos hacer el llamado desde main que se encuentra en la clase App.java lo que nos quedara así

```
package ni.gacssoft;
import static ni.gacssoft.Util.getToday;

/**
 * Hello world!
 * @author gacs
 */
public class App 
{
    public static void main( String[] args )
    {
        System.out.println( "Hola Mundo!" );
        System.out.println( getToday() );
    }
}
```

Agregamos los cambios, creamos el commit y cerramos la rama feature/today

```
git add App.java
git commit -m"Se modifica la clase App.java se implementa el llamado al metodo getToday()"
git flow feature finish feature/today
```
Procederemos enviar los cambios a producción con la versión 1.2.0., agregaremos el archivo CHANGELOG.TXT, el cual llevara las nuevas implementaciones de esta versión.
```
git log --oneline --no-merges master...HEAD --pretty=format:" %s "  >  CHANGELOG.txt
```
Agregamos los cambios, creamos el commit correspondiente y enviamos a producción la versión 1.2.0 de HW.
```
git add CHANGELOG.TXT
git commit -m"Version hw1.2.0"
git flow release finish release/hw1.2.0
```
Nos piden la versión hw2.0.0, pero esta ves el saludo sera al usuario de la maquina donde se ejecute el programa y que se implemente la librería jfiglet.
Creamos la rama feature/Huser
```
git flow feature star feature/Huser
```
Modificamos el archivo pom.xml agregando la dependencias y las configuraciones de compilación, el cual nos queda así:
```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>ni.gacssoft</groupId>
  <artifactId>hw</artifactId>
  <packaging>jar</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>hw</name>
  <url>http://maven.apache.org</url>


	  <dependencies>
	    <dependency>
	      <groupId>junit</groupId>
	      <artifactId>junit</artifactId>
	      <version>4.12</version>
	      <scope>test</scope>
	    </dependency>

	<!-- https://mvnrepository.com/artifact/com.github.lalyos/jfiglet -->
	<dependency>
	    <groupId>com.github.lalyos</groupId>
	    <artifactId>jfiglet</artifactId>
	    <version>0.0.8</version>
	</dependency>

	  </dependencies>
    <build>
        <plugins>
            <!-- Crear un fat jar -->
            <plugin>
                <artifactId>maven-assembly-plugin</artifactId>
                <version>3.1.1</version>
                <configuration>
                    <!-- Clase principal -->
                    <archive>
                        <manifest>
							<addClasspath>true</addClasspath>
                            <mainClass>ni.gacssoft.App</mainClass>
                        </manifest>
                    </archive>
                    <descriptorRefs>
                        <descriptorRef>jar-with-dependencies</descriptorRef>
                    </descriptorRefs>
                </configuration>
                <executions>
                    <execution>
                        <id>assemble-all</id>
                        <phase>package</phase> 
                        <goals>
                            <goal>single</goal>
                        </goals>
                    </execution>
                </executions>
            </plugin>
        </plugins>
    </build>

	 <properties> 
	        <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding>
	        <project.reporting.outputEncoding>UTF-8</project.reporting.outputEncoding>
	        <maven.compiler.source>10</maven.compiler.source>
	        <maven.compiler.target>10</maven.compiler.target>
	</properties> 


</project>
```
Agregamos las modificaciones y creamos el commit correspondiente.
```
git add pom.xml
git commit -m"Se actualiza pom.xml con dependencias jfiglet y configuracion para compilacion con dependicas"
```
Modificamos el archivo App.java aplicando las mejoras solicitadas, nos quedara así:
```
package ni.gacssoft;
import static ni.gacssoft.Util.getToday;
import com.github.lalyos.jfiglet.FigletFont;
import java.io.IOException;

/**
 * Hello world!
 * @author gacs
 * @version 2.0.0
 */
public class App 
{
    public static void main( String[] args ) throws IOException
    {
	String strHW = FigletFont.convertOneLine("Hola "+System.getProperty("user.name"));
//        System.out.println( "Hola Mundo!" );
        System.out.println( strHW );
        System.out.println( getToday() );
    }
}
```
Agregamos las modificaciones, creamos el commit correspondiente, cerramos el feature/Huser y enviamos las mejoras a producción.
```
git add App.java
git commit -m"Se modifica la clase App.java se cambia el saludo de Hola Mundo a Hola <user> utilizando la liberia jfiglet"
git flow feature finish feature/Huser
git flow release start release/hw2.0.0
git log --oneline --no-merges master...HEAD --pretty=format:" %s "  >  CHANGELOG.txt
git add CHANGELOG.TXT
git commit -m"Version hw2.0.0"
git flow release finish release/hw2.0.0
```
