Project.clj SPEC
================

The relatively new Clojure eco-system already sports 3 build systems which rely
on a project.clj file: Cake, Lein and Polyglot Maven.

All three of these have (or are bound to have) subtle differences in the way they
consume/understand the project.clj as there is no standard specification. This
project aims to provide that specification.

Ideally if the implementer of an IDE wants to rely on information
in the project.clj, he should not have to cater specifically to all 3 build systems
but rather code to this spec and the build systems should ensure compatability.

    (defproject name-as-SYMBOL-OR-STRING version-as-STRING
        keyword value)

    Example:

    (defproject build-spec "0.0.1"
        :option value)

The keywords can be the following and accept values of the type described below


<table>
  <tr>
   <td>Keyword</td>
   <td>Description</td>
   <td>Type</td>
   <td>Example</td>
  </tr>
  <tr>
   <td>:description</td>
   <td>Description of the Project</td>
   <td>String</td>
   <td>"My project"</td>
  </tr>
  <tr>
   <td>:main</td>
   <td>Namespace for Jar/War files main entry</td>
   <td>Symbol</td>
   <td>project.core</td>
  </tr>
  <tr>
   <td>:namespaces</td>
   <td>Namespaces to be AOT compiled</td>
   <td>Vector of Symbols</td>
   <td>[namespace1 namespace2]</td>
  </tr>
  <tr>
   <td>:repositories</td>
   <td>List of Maven repositories used to fetch dependencies</td>
   <td>Vector of Vectors of Strings</td>
   <td>[["maven2-repository.dev.java.net" "http://download.java.net/maven/2/"]]</td>
  </tr>
  <tr>
   <td>:dependencies</td>
   <td>List of project dependencies</td>
   <td>Vector of (Vectors with group-id as symbol and version as string) OR (Vectors of strings)</td>
   <td>[[org.clojure/clojure "1.2.0"]] OR
       [["org.clojure/clojure-1.2.0"]]
   </td>
  </tr>
  <tr>
   <td>:dev-dependencies</td>
   <td>List of project development dependencies</td>
   <td>Vector of (Vectors with group-id as symbol and version as string) OR (Vectors of strings)</td>
   <td>[[org.clojure/clojure "1.2.0"]] OR
       [["org.clojure/clojure-1.2.0"]]
   </td>
  </tr>
  <tr>
   <td>:jar-files</td>
   <td>List of folders to be embedded in jar-files</td>
   <td>Vector of Vectors of 2 strings. First string is physical folder, the second is path in the jar files</td>
   <td>:jar-files [["resources" ""]] (will make project/resources/file.clj appear as /file.clj in the jar-file)</td>
  </tr>
  <tr>
   <td>:war-files</td>
   <td>List of folders to be embedded in war-files</td>
   <td>Vector of Vectors of 2 strings. First string is physical folder, the second is path in the war files</td>
   <td>:jar-files [["resources" ""]] (will make project/resources/file.clj appear as /file.clj in the jar-file)</td>
  </tr>
  <tr>
   <td>:omit-source</td>
   <td>Boolean to determine if source is omitted from jar/war files</td>
   <td>Boolean (true or false)</td>
   <td>:omit-source true</td>
  </tr>
  <tr>
   <td>:aot</td>
   <td>Enum to enable AOT compilation of all namespaces</td>
   <td>:all</td>
   <td>:aot :all</td>
  </tr>


</table>
