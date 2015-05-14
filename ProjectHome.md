<p><strong>log4jdbc-log4j2</strong> is a modification of <a href='http://code.google.com/p/log4jdbc/' title='External link to log4jdbc'>log4jdbc</a> to natively use Log4j 2 (or SLF4J as usual), that supports JDBC 4.1 to JDBC 3, includes all the improvements of log4jdbc-remix, and provides new improvements on its own. log4jdbc-log4j2:<br>
<ul>
<li>natively supports <a href='http://logging.apache.org/log4j/2.x/' title='External link to log4j 2'>Log4j 2</a>. <a href='http://www.slf4j.org/' title='External link to SLF4J'>SLF4J</a> can still be used as usual.</li>
<li>supports JDBC 4.1 (Java 7), JDBC 4 (Java 6), JDBC 3 (Java 5).</li>
<li>includes all the improvements of <a href='http://code.google.com/p/log4jdbc-remix/' title='External link to log4jdbc-remix'>log4jdbc-remix</a> (can log result sets as tables, can be configured as a <code>Datasource</code>, can use a plugable SQL formatter).</li>
<li>is available in the sonatype maven repository.</li>
<li>provides new improvements on its own (logging of connection opening execution time, of <code>getGeneratedKeys()</code> queries, etc)</li>
</ul>
<br>
<br>
<hr /><br>
<br>
<br>
<br>
<h1>News</h1>
<ul>
<li><strong>2013-12-12: </strong>Release of log4jdbc-logj2 1.16: fixes <a href='https://code.google.com/p/log4jdbc-log4j2/issues/detail?id=#8'>issue #8</a>, <a href='https://code.google.com/p/log4jdbc-log4j2/issues/detail?id=#9'>issue #9</a>, and <a href='https://code.google.com/p/log4jdbc-log4j2/issues/detail?id=#10'>issue #10</a>.</li>

<li><strong>2013-06-21: </strong>Release of log4jdbc-logj2 1.15: several bug fixes related to the print of the result sets as table (because of modifications in this implementation as compared to log4jdbc-remix).</li>

<li><strong>2013-06-20: </strong>Release of log4jdbc-logj2 1.14: bug fixes and improvements from the log4jdbc-remix trunk, notably the ability to provide different SQL loggers to different data sources (see <a href='http://code.google.com/p/log4jdbc-remix/issues/detail?id=9'>http://code.google.com/p/log4jdbc-remix/issues/detail?id=9</a>).</li>

<li><strong>2013-06-19: </strong>Release of log4jdbc-logj2 1.13: bug fix (see <a href='https://code.google.com/p/log4jdbc-log4j2/issues/detail?id=#4'>issue #4</a>).</li>

<li><strong>2013-04-25: </strong>Release of log4jdbc-logj2 1.12: Adding fixes that were committed to the main log4jdbc branch after the last official release.</li>

<li><strong>2013-04-23: </strong>Release of log4jdbc-logj2 1.11: Clearer error message when no proper logging system can be found. Availability on the Sonatype maven repository (finally!).</li>

<li><strong>2013-03-31: </strong>Release of log4jdbc-logj2 1.1: Major update to include all the improvements of log4jdbc-remix, provide support for JDBC 4.1, to allow the use of solely one logger library (either Log4j 2 or SLF4J), and to add several unit tests.</li>

<li><strong>2012-11-14: </strong>Release of log4jdbc-logj2 1.01: minor modification to adapt to a change of API in log4j 2.0 beta2 (the previous release was based on log4j 2.0 alpha2 SNAPSHOT)</li>

<li><strong>2012-09-05: </strong>log4jdbc-logj2 1.0 is out.</li>
</ul>
<br>
<br>
<hr /><br>
<br>
<br>
<br>
<h1>Advantages</h1>
<h2>One single logger</h2>
<p>Thanks to the use of the features provided by Log4j 2, only one single logger is needed to be configured, as opposed to five in the standard implementation of log4jdbc (and six when using log4jdbc-remix). The standard log4jdbc behavior can still be easily reproduced (see below for more details). You can nevertheless use SLF4J and configure several loggers as in the standard log4jdbc implementation if you wish to do so.</p>

<h2>log4jdbc-remix features</h2>
<p>All the improvements provided by log4jdbc-remix are included in this implementation: can log result sets as tables, can be configured as a <code>Datasource</code>, can use a custom SQL formatter, is available in the sonatype maven repository. If you use Log4j 2, the logging of the result sets are still configurable with a single logger. Also note that this implementation provides an additional way of configuring a custom SQL formatter, through properties (see below).</p>

<h2>JDBC 4.1 support</h2>
log4jdbc-log4j2 supports JDBC 4.1 (JDK 1.7), JDBC 4 (JDK 1.6), JDBC 3 (JDK 1.5). Please note that we do not provide a JDBC 3 version for JDK 1.4.<br>
<br>
<h2>Easy dispatch in different files of different SQL operations</h2>
<p>Thanks to the use of the features provided by Log4j 2, you can easily dispatch different SQL operations (SELECT, UPDATE, ...) or errors (Exception thrown) in different files . This is not doable using the standard implementation of log4jdbc.</p>

<h2>Availability in the sonatype maven repository</h2>
<p>log4jdbc-log4j2 is available through the Maven repository: group <code>org.bgee.log4jdbc-log4j2</code>, artifacts <code>log4jdbc-log4j2-jdbc3</code>, <code>log4jdbc-log4j2-jdbc4</code>, and <code>log4jdbc-log4j2-jdbc4.1</code>.</p>

<h2>Other improvements</h2>
<p>This implementation provides some slight improvements, for instance: execution time for connection opening and closing, calls to <code>Statement.getGeneratedKeys()</code> logged along with the SQL query it was performed on, etc.</p>
<br>
<br>
<hr /><br>
<br>
<br>
<br>
<h1>Installation</h1>
Installation is almost the same as with the standard version of log4jdbc. <strong>But be careful with the slight modifications</strong>, notably:<br>
<ul>
<li>the name of the <code>Driver</code> to load is different than in the standard log4jdbc implementation (but if you use the JDBC 4 or JDBC 4.1 versions, you do not need to load the <code>Driver</code> yourself anyway, log4jdbc-log4j2 will be automatically discovered and loaded).</li>
<li>If you choose to use SLF4J rather than Log4j 2, you need to configure the option <code>log4jdbc.spylogdelegator.name</code> to the value <code>net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator</code> (see below for more details).</li>
</ul>

<h2>1. Install log4jdbc-log4j2</h2>
<h3>1.1. Decide if you need JDBC 3, JDBC 4, or JDBC 4.1 support.</h3>
<p>Depending on which JDK you use, you should install different versions of log4jdbc-log4j2:<br>
<ul>
<li>If you are using Java 5, you should use the JDBC 3 version of log4jdbc-log4j2.</li>
<li>For Java 6, the JDBC 4 version of log4jdbc-log4j2.</li>
<li>For Java 7, the JDBC 4.1 version of log4jdbc-log4j2.</li>
</ul>

You should make your choice based on which JDK version you use, rather than which JDBC version: for instance, the log4jdbc JDBC 4 driver can wrap a JDBC 3 or older driver, as long as you don't call any unsupported method.<br>
</p>

<h3>1.2. Option 1: installation via direct download</h3>
<p>Choose and download one of the driver .jar files:<br>
<ul>
<li><a href='http://log4jdbc-log4j2.googlecode.com/files/log4jdbc-log4j2-jdbc3-1.16.jar' title='Download log4jdbc-log4j2 for JDBC3'>log4jdbc-log4j2-jdbc3.jar</a> for JDBC 3 support in JDK 1.5. Please note that starting from version <code>beta5</code>, Log4j 2 is compiled using JDK 1.6, so that log4jdbc-log4j2 for JDBC3 is usable with no later version than Log4j 2 <code>beta4</code>.</li>
<li><a href='http://log4jdbc-log4j2.googlecode.com/files/log4jdbc-log4j2-jdbc4-1.16.jar' title='Download log4jdbc-log4j2 for JDBC4'>log4jdbc-log4j2-jdbc4.jar</a> for JDBC 4 support in JDK 1.6</li>
<li><a href='http://log4jdbc-log4j2.googlecode.com/files/log4jdbc-log4j2-jdbc4.1-1.16.jar' title='Download log4jdbc-log4j2 for JDBC4.1'>log4jdbc-log4j2-jdbc4.1.jar</a> for JDBC 4.1 support in JDK 1.7</li>
</ul>
Place the log4jdbc-log4j2 jar that you chose into your application's classpath.</p>

<h3>1.3. Option 2: installation via Maven repository</h3>
Add the following to your <code>pom.xml</code> configuration file, replace <code>log4jdbc-log4j2-jdbcXX</code> by the value corresponding to the JDBC version you want to use (either <code>log4jdbc-log4j2-jdbc4.1</code>, or <code>log4jdbc-log4j2-jdbc4</code>, or <code>log4jdbc-log4j2-jdbc3</code>):<br>
<pre><code>&lt;dependency&gt;<br>
  &lt;groupId&gt;org.bgee.log4jdbc-log4j2&lt;/groupId&gt;<br>
  &lt;artifactId&gt;log4jdbc-log4j2-jdbcXX&lt;/artifactId&gt;<br>
  &lt;version&gt;1.16&lt;/version&gt;<br>
&lt;/dependency&gt;<br>
</code></pre>

<h2>2. Install the logging library you want to use</h2>
<h3>2.1. If you want to use Log4j 2 (recommended choice)</h3>
<p>Get the last version of Log4j 2, either from their <a href='http://logging.apache.org/log4j/2.0/download.html' title='External link to log4j 2'>download page</a>, or from their <a href='http://logging.apache.org/log4j/2.x/build.html' title='External link to log4j 2'>Maven repository</a> (this link contains instructions to configure your <code>pom.xml</code> file).</p>

<p>You will typically need to install the <code>log4j-core</code> and <code>log4j-api</code> libraries. Please note that starting from version <code>beta5</code>, Log4j 2 is compiled using JDK 1.6, so that log4jdbc-log4j2 for JDBC3 is usable with no later version than Log4j 2 <code>beta4</code>.</p>

<h3>2.2. If you want to use SLF4J</h3>
<p>Get the last version of SLF4J, either from their <a href='http://www.slf4j.org/download.html' title='External link to SLF4J'>download page</a>, or from their <a href='http://mvnrepository.com/artifact/org.slf4j' title='SLF4J Maven repository'>Maven repository</a>. </p>

<p>You will need at least two libraries: the <code>slf4j-api</code> library, and whichever library you pick depending on the java logging system you choose (for instance, Log4j, java.util logging, logback, Jakarta Commons Logging).<br>
<br>
<h2>3. Modification of your source code</h2>
<h3>3.1. Change your JDBC URL</h3>
Prepend <strong><code>jdbc:log4</code></strong> to the normal JDBC URL that you are using.<br>
For example, if your normal JDBC URL is:<br>
<pre><code>      jdbc:derby://localhost:1527//db-derby-10.2.2.0-bin/databases/MyDatabase<br>
</code></pre>
then you would change it to:<br>
<pre><code>      jdbc:log4jdbc:derby://localhost:1527//db-derby-10.2.2.0-bin/databases/MyDatabase<br>
</code></pre>
to use log4jdbc-log4j2.<br>
<br>
<h3>3.2. Change the driver used</h3>
<p>Set your JDBC driver class to <strong><code>net.sf.log4jdbc.sql.jdbcapi.DriverSpy</code></strong> in your application (please note that this is not the same class name as in the standard log4jdbc implementation). See the <a href='http://code.google.com/p/log4jdbc/' title='External link to log4jdbc'>log4jdbc documentation</a> to see the list of supported drivers, or how to add support for other drivers. log4jdbc supports almost all major drivers.</p>
<p>Note that it is actually not necessary to set the <code>Driver</code> to load (through, for instance, <code>Class.forName("net.sf.log4jdbc.sql.jdbcapi.DriverSpy")</code>) if you use the JDBC 4 or JDBC 4.1 versions. The driver will be automatically discovered and loaded.</p>

<h2>4. Set up your logger</h2>
<h3>4.1. If you use Log4j 2</h3>
<p>Log4jdbc-log4j2 uses only one logger, called <strong><code>log4jdbc.log4j2</code></strong> (while the standard implementation uses 5, and even 6 when using log4jdbc-remix).</p>
<p>Its behavior can be set, notably from a Log4j 2 configuration file. This documentation presents some examples (see "Usage" below). Almost all features provided by the standard implementations of log4jdbc and log4jdbc-remix can be reproduced by using this single logger, thanks to the use of <a href='http://logging.apache.org/log4j/2.0/manual/markers.html'>Markers</a>.</p>
<p>This allows a very simple configuration, for instance, at the <code>ERROR</code> level:<br>
<pre><code>&lt;logger name="log4jdbc.log4j2" level="error" additivity="false"&gt;<br>
  &lt;appender-ref ref="Console"/&gt;<br>
&lt;/logger&gt;<br>
</code></pre>
And that's it!</p>

<p>This logger is easily configurable via the use of <code>Marker</code>s. See the "Usage" section below for several examples on how to use them, or how to reproduce log4jdbc and log4jdbc-remix standard behaviors. The recommended configuration at <code>INFO</code> or <code>DEBUG</code> level is basically:<br>
<pre><code>&lt;logger name="log4jdbc.log4j2" level="info" additivity="false"&gt;<br>
  &lt;MarkerFilter marker="LOG4JDBC_OTHER" onMatch="DENY" onMismatch="NEUTRAL"/&gt;<br>
  &lt;appender-ref ref="Console"/&gt;<br>
&lt;/logger&gt;<br>
</code></pre>
</p>

<p>Note that if this logger is turned off (or for example, set to a level less than error, such as the FATAL level), then log4jdbc will not log anything and in fact the actual real connection to the underlying database will be returned by the log4jdbc driver (thus allowing log4jdbc to be installed and available to turn on at runtime at a moment's notice without imposing any actual performance loss when not being used).</p>
<h4>List of all available <code>Marker</code>s</h4>
<ul>
<li><code>LOG4JDBC_EXCEPTION</code>: associated to all <code>SQLException</code>s. This is useful when the feature of logging slow queries with an <code>ERROR</code> level is activated.</li>

<li><code>LOG4JDBC_SQL</code>: associated to SQL statements (to <strong>all</strong> statements, even different operations than select, update, insert, delete, or create, for instance: drop). Parent of the following markers:<br>
<ul>
<li><code>LOG4JDBC_SELECT</code>: associated to SQL statements performing a <code>SELECT</code> operation.</li>
<li><code>LOG4JDBC_UPDATE</code>: associated to SQL statements performing a <code>UPDATE</code> operation.</li>
<li><code>LOG4JDBC_INSERT</code>: associated to SQL statements performing a <code>INSERT</code> operation.</li>
<li><code>LOG4JDBC_DELETE</code>: associated to SQL statements performing a <code>DELETE</code> operation.</li>
<li><code>LOG4JDBC_CREATE</code>: associated to SQL statements performing a <code>CREATE</code> operation.</li>
</ul>
</li>

<li><code>LOG4JDBC_NON_STATEMENT</code>: associated to all JDBC calls that are not SQL statements, and to the logging of result sets as tables (log4jdbc-remix feature). Parent of the following markers:<br>
<ul>

<li><code>LOG4JDBC_CONNECTION</code>: logs connection open, close, and abort events, as well as dump of all open connection numbers (useful for hunting down connection leak problems).</li>

<li><code>LOG4JDBC_OTHER</code>: associated to all JDBC calls, including calls to <code>ResultSet</code>, and to the logging of result sets as tables (log4jdbc-remix feature). Parent of the following markers:<br>
<ul>

<li><code>LOG4JDBC_JDBC</code>: associated to all JDBC calls, including calls to <code>ResultSet</code>. Parent of the following markers:<br>
<ul>
<li><code>LOG4JDBC_AUDIT</code>: associated to JDBC calls, except calls to <code>ResultSet</code>. This is a very voluminous output, and is not normally needed unless tracking down a specific JDBC problem.</li>
<li><code>LOG4JDBC_RESULTSET</code>: associated to calls to <code>ResultSet</code>. Produce logs even more voluminous, because all calls to ResultSet objects are logged.</li>

</ul>
</li>
<li><code>LOG4JDBC_RESULTSETTABLE</code>: <code>Marker</code> to log JDBC <code>ResultSet</code>s as table. Functionality inherited from log4jdbc-remix (corresponds to the <code>jdbc.resultsettable</code> logger in the log4jdbc-remix implementation)</li>
</ul>
</li>
</ul>
</li>
</ul>


<h3>4.2. If you use SLF4J</h3>
<h4>4.2.1 Set the option <code>log4jdbc.spylogdelegator.name</code></h4>
<p>First, you need to tell log4jdbc-log4j2 that you want to use the SLF4J logger. You need to configure the option <code>log4jdbc.spylogdelegator.name</code> to the value <code>net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator</code>. This is done either via the <strong><code>log4jdbc.log4j2.properties</code></strong> file stored in your classpath, or via system properties.</p>
<p>Add to the <code>log4jdbc.log4j2.properties</code> file:<br>
<pre><code>log4jdbc.spylogdelegator.name=net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator<br>
</code></pre>
</p>
<p>Or use System properties:<br>
<pre><code>java -Dlog4jdbc.spylogdelegator.name=net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator -classpath ./classes my.funky.Program<br>
</code></pre>
</p>
<p>See below for more details about how to configure the options of log4jdbc-log4j2 (notably, the <code>log4jdbc.spylogdelegator.name</code> option allows to set any custom SQL formatter).</p>

<h4>4.2.2. Configure the loggers</h4>
<p>From the log4jdbc and log4jdbc-remix documentation: there are 6 loggers that are used. If all 6 are turned off (or for example, set to a level less than error, such as the FATAL level in log4j), then log4jdbc will not log anything and in fact the actual (real) connection to the underlying database will be returned by the log4jdbc driver (thus allowing log4jdbc to be installed and available to turn on at runtime at a moment's notice without imposing any actual performance loss when not being used). If any of the 5 logs are set to ERROR level or above (e.g ERROR, INFO or DEBUG) then log4jdbc will be activated, wrapping and logging activity in the JDBC connections returned by the underlying driver.</p>
<table><thead><th><strong>logger</strong></th><th><strong>description</strong></th></thead><tbody>
<tr><td>jdbc.sqlonly</td><td>Logs only SQL. SQL executed within a prepared statement is automatically shown with it's bind arguments replaced with the data bound at that position, for greatly increased readability. </td></tr>
<tr><td>jdbc.sqltiming</td><td>Logs the SQL, post-execution, including timing statistics on how long the SQL took to execute. </td></tr>
<tr><td>jdbc.audit</td><td>Logs ALL JDBC calls except for ResultSets. This is a very voluminous output, and is not normally needed unless tracking down a specific JDBC problem. </td></tr>
<tr><td>jdbc.resultset</td><td>Even more voluminous, because all calls to ResultSet objects are logged. </td></tr>
<tr><td>jdbc.resultsettable</td><td>Log the jdbc results as a table. Level debug will fill in unread values in the result set. </td></tr>
<tr><td>jdbc.connection</td><td>Logs connection open and close events as well as dumping all open connection numbers. This is very useful for hunting down connection leak problems. </td></tr></tbody></table>

<h3>  4.3. For both Log4j 2 or SLF4J</h3>
<p>The levels used are the same as in the standard implementation:<br>
<ul><li><code>DEBUG</code> includes the class name and line number (if available) at which the SQL was executed. <strong>Use DEBUG level with extra care, as this imposes an additional performance penalty when in use.</strong>
</li><li><code>INFO</code> includes the SQL (or other information as applicable.)<br>
</li><li><code>ERROR</code> includes the stack traces in the log output when <code>SQLException</code>s occur (and slow queries if enabled, see below).<br>
</p>
<p>Additionally, there is one logger named log4jdbc.debug which is for use with internal debugging of log4jdbc. At this time it just prints out information on which underlying drivers were found and not found when the log4jdbc spy driver loads. </p>
<br>
<br>
<hr /><br>
<br>
</li></ul>

<h1>Usage with Log4j 2</h1>
These examples assume that you configure Log4j 2 through a <code>log4j2.xml</code> configuration file, placed in your classpath.<br>
<h2>1. Basic configuration at <code>ERROR</code> level</h2>
An example Log4j 2 configuration file: uses the <code>log4jdbc.log4j2</code> logger, and writes errors (and slow queries if enabled, see below) into the file <code>log4jdbc.out</code>:<br>
<pre><code>&lt;?xml version="1.0" encoding="UTF-8"?&gt;<br>
&lt;configuration status="OFF"&gt;<br>
  &lt;appenders&gt;<br>
    &lt;Console name="Console" target="SYSTEM_OUT"&gt;<br>
      &lt;PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %level - %m%n%ex%n"/&gt;<br>
    &lt;/Console&gt;<br>
    &lt;File name="log4jdbc_file" fileName="log4jdbc.out"&gt;<br>
      &lt;PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %level - %m%n%ex%n"/&gt;<br>
    &lt;/File&gt;<br>
  &lt;/appenders&gt;<br>
  &lt;loggers&gt;<br>
    &lt;root level="off"&gt;<br>
      &lt;appender-ref ref="Console"/&gt;<br>
    &lt;/root&gt;<br>
    &lt;logger name="log4jdbc.log4j2" level="error" additivity="false"&gt;<br>
      &lt;appender-ref ref="log4jdbc_file"/&gt;<br>
    &lt;/logger&gt;<br>
  &lt;/loggers&gt;<br>
&lt;/configuration&gt;<br>
</code></pre>
<h2>2. Recommended configuration at <code>INFO</code> or <code>DEBUG</code> level</h2>
This modified implementation uses <a href='http://logging.apache.org/log4j/2.0/manual/markers.html'>Markers</a>, rather than different loggers as in the standard implementation. Here is a configuration example at <code>INFO</code> or <code>DEBUG</code> level, to log all relevant information (SQL statements, Connection calls, Exceptions thrown), and to not log JDBC calls, nor result sets as tables (overwhelming logs). It is just a matter of adding one line (<code>&lt;MarkerFilter...</code>):<br>
<pre><code>&lt;logger name="log4jdbc.log4j2" level="info" additivity="false"&gt;<br>
  &lt;MarkerFilter marker="LOG4JDBC_OTHER" onMatch="DENY" onMismatch="NEUTRAL"/&gt;<br>
  &lt;appender-ref ref="log4jdbc_file"/&gt;<br>
&lt;/logger&gt;<br>
</code></pre>

<h2>3. Recommended configuration at <code>INFO</code> or <code>DEBUG</code> level, when additionally logging result sets as tables (log4jdbc-remix feature)</h2>
This configuration will log all relevant information (SQL statements, Connection calls, Exceptions thrown), as well as result sets as tables (log4jdbc-remix feature):<br>
<pre><code>&lt;logger name="log4jdbc.log4j2" level="info" additivity="false"&gt;<br>
  &lt;MarkerFilter marker="LOG4JDBC_JDBC" onMatch="DENY" onMismatch="NEUTRAL"/&gt;<br>
  &lt;appender-ref ref="log4jdbc_file"/&gt;<br>
&lt;/logger&gt;<br>
</code></pre>

<h2>4. Reproducing standard log4jdbc and log4jdbc-remix behaviors</h2>
Log4jdbc and log4jdbc-remix uses 6 loggers to log different information (see the log4jdbc documentation). This modified implementation rather uses <a href='http://logging.apache.org/log4j/2.0/manual/markers.html'>Markers</a> to achieve the same operations. Here are the configurations to reproduce the log4jdbc and log4jdbc-remix loggers behaviors:<br>
<ul><li><code>jdbc.sqltiming</code>: logs SQL statements with execution time, does not log <code>Connection</code> calls, nor JDBC and <code>ResultSet</code> calls.<br>
<pre><code>    &lt;logger name="log4jdbc.log4j2" level="info" additivity="false"&gt;<br>
      &lt;MarkerFilter marker="LOG4JDBC_NON_STATEMENT" onMatch="DENY" onMismatch="NEUTRAL"/&gt;<br>
      &lt;appender-ref ref="log4jdbc_file"/&gt;<br>
    &lt;/logger&gt;<br>
</code></pre>
</li><li><code>jdbc.audit</code>: logs all JDBC calls except for <code>ResultSet</code>s.<br>
<pre><code>    &lt;logger name="log4jdbc.log4j2" level="info" additivity="false"&gt;<br>
      &lt;MarkerFilter marker="LOG4JDBC_AUDIT" onMatch="ACCEPT" onMismatch="DENY"/&gt;<br>
      &lt;appender-ref ref="log4jdbc_file"/&gt;<br>
    &lt;/logger&gt;<br>
</code></pre>
</li><li><code>jdbc.resultset</code>: logs <code>ResultSet</code> calls.<br>
<pre><code>    &lt;logger name="log4jdbc.log4j2" level="info" additivity="false"&gt;<br>
      &lt;MarkerFilter marker="LOG4JDBC_RESULTSET" onMatch="ACCEPT" onMismatch="DENY"/&gt;<br>
      &lt;appender-ref ref="log4jdbc_file"/&gt;<br>
    &lt;/logger&gt;<br>
</code></pre>
</li><li><code>jdbc.connection</code>: logs connection calls.<br>
<pre><code>    &lt;logger name="log4jdbc.log4j2" level="info" additivity="false"&gt;<br>
      &lt;MarkerFilter marker="LOG4JDBC_CONNECTION" onMatch="ACCEPT" onMismatch="DENY"/&gt;<br>
      &lt;appender-ref ref="log4jdbc_file"/&gt;<br>
    &lt;/logger&gt;<br>
</code></pre>
</li><li><code>jdbc.resultsettable</code>: Log the jdbc results as a table (log4jdbc-remix feature). Level debug will fill in unread values in the result set.<br>
<pre><code>    &lt;logger name="log4jdbc.log4j2" level="info" additivity="false"&gt;<br>
      &lt;MarkerFilter marker="LOG4JDBC_RESULTSETTABLE" onMatch="ACCEPT" onMismatch="DENY"/&gt;<br>
      &lt;appender-ref ref="log4jdbc_file"/&gt;<br>
    &lt;/logger&gt;<br>
</code></pre>
</li><li><code>jdbc.sqlonly</code>: the behavior of this logger is not implemented. This is for the will of keeping one single logger, while the logging of events immediately, before the action is executed and before knowing the execution time, would definitely require another logger, or a completely different system of Markers. Also, execution time seems to be an always-useful information to get.</li></ul>

<h2>5. Disabling some SQL operations, or dispatching them in different files</h2>
<p>The standard implementation of log4jdbc allows to disable the logging of some SQL operations, through the configuration of log4jdbc properties (<code>log4jdbc.dump.sql.select</code>, <code>log4jdbc.dump.sql.insert</code>, <code>log4jdbc.dump.sql.update</code>, <code>log4jdbc.dump.sql.create</code>, <code>log4jdbc.dump.sql.delete</code>).</p>
<p>The same feature is implemented through the use of <code>Marker</code>s (<code>LOG4JDBC_SELECT</code>, <code>LOG4JDBC_INSERT</code>, <code>LOG4JDBC_UPDATE</code>, <code>LOG4JDBC_CREATE</code>, <code>LOG4JDBC_DELETE</code>). This has the advantage to also allow the dispatch of different operations in different files. Note that the log4jdbc properties can still be set, and have priority over the <code>Marker</code>s.</p>
<p>Here is an example configuration file to disable the logging of <code>select</code> operations, while dispatching <code>update</code> operations in one file, all other statements in another one: </p>
<pre><code>&lt;?xml version="1.0" encoding="UTF-8"?&gt;<br>
&lt;configuration status="OFF"&gt;<br>
  &lt;appenders&gt;<br>
    &lt;Console name="Console" target="SYSTEM_OUT"&gt;<br>
      &lt;PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %level - %m%n%ex%n"/&gt;<br>
    &lt;/Console&gt;<br>
    &lt;File name="log4jdbc_update" fileName="log4jdbc_update.out"&gt;<br>
      &lt;MarkerFilter marker="LOG4JDBC_UPDATE" onMatch="ACCEPT" onMismatch="DENY"/&gt;<br>
      &lt;PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %level - %m%n%ex%n"/&gt;<br>
    &lt;/File&gt;<br>
    &lt;File name="log4jdbc_file" fileName="log4jdbc.out"&gt;<br>
      &lt;MarkerFilter marker="LOG4JDBC_UPDATE" onMatch="DENY" onMismatch="NEUTRAL"/&gt;<br>
      &lt;PatternLayout pattern="%d{HH:mm:ss.SSS} [%t] %level - %m%n%ex%n"/&gt;<br>
    &lt;/File&gt;<br>
  &lt;/appenders&gt;<br>
  &lt;loggers&gt;<br>
    &lt;root level="off"&gt;<br>
      &lt;appender-ref ref="Console"/&gt;<br>
    &lt;/root&gt;<br>
    &lt;logger name="log4jdbc.log4j2" level="info" additivity="false"&gt;<br>
      &lt;MarkerFilter marker="LOG4JDBC_SELECT" onMatch="DENY" onMismatch="NEUTRAL"/&gt;<br>
      &lt;appender-ref ref="log4jdbc_file"/&gt;<br>
      &lt;appender-ref ref="log4jdbc_update"/&gt;<br>
    &lt;/logger&gt;<br>
  &lt;/loggers&gt;<br>
&lt;/configuration&gt;<br>
</code></pre>
<p>In a similar way, <code>SQLException</code>s can be sent to a separate file, using the <code>Marker</code> <code>LOG4JDBC_EXCEPTION</code> (this is useful when the feature of logging slow queries with an <code>ERROR</code> level is activated; in this case, an error is not always associated to an <code>Exception</code>).</p>

<br>
<br>
<hr /><br>
<br>
<br>
<br>
<h1>Configure a <code>DataSource</code></h1>
<h2>Option 1: configure Driver class name and JDBC URL</h2>
<p>You can either configure your <code>DataSource</code> to use the log4jdbc-log4j2 driver (<strong><code>net.sf.log4jdbc.sql.jdbcapi.DriverSpy</code></strong>), and to use the modified JDBC URL (prepending <strong><code>jdbc:log4</code></strong> to the normal JDBC URL).</p>

<h2>Option 2: wrap into the log4jdbc <code>DataSource</code></h2>
<p>Or you can wrap your own <code>DataSource</code> into the log4jdbc-log4j2 <code>DataSource</code>. For instance (from the log4jdbc-remix documentation), if you have:<br>
<pre><code>  &lt;bean id="dataSource" class="..."&gt;<br>
    &lt;property name="driverClass" value="${datasource.driverClassName}"/&gt;<br>
    &lt;property name="jdbcUrl" value="${datasource.url}"/&gt;<br>
    &lt;property name="user" value="${datasource.username}"/&gt;<br>
    &lt;property name="password" value="${datasource.password}"/&gt;<br>
    ...<br>
  &lt;/bean&gt;<br>
</code></pre>
Change this to<br>
<pre><code>  &lt;bean id="dataSourceSpied" class="..."&gt;<br>
    &lt;property name="driverClass" value="${datasource.driverClassName}"/&gt;<br>
    &lt;property name="jdbcUrl" value="${datasource.url}"/&gt;<br>
    &lt;property name="user" value="${datasource.username}"/&gt;<br>
    &lt;property name="password" value="${datasource.password}"/&gt;<br>
    ...<br>
  &lt;/bean&gt;<br>
<br>
  &lt;bean id="dataSource" class="net.sf.log4jdbc.sql.jdbcapi.DataSourceSpy"&gt;<br>
    &lt;constructor-arg ref="dataSourceSpied" /&gt;<br>
  &lt;/bean&gt;<br>
</code></pre>
</p>
<br>
<br>
<hr /><br>
<br>
<br>
<br>
<h1>Custom SQL formatter</h1>
<p>As with log4jdbc-remix, it is possible to provide you own custom log formatter. Your logger must implement the interface <code>net.sf.log4jdbc.log.SpyLogDelegator</code>. To make log4jdbc-log4j2 to use it, you have different options:<br>
<ul>
<li><strong>Option 1</strong> (recommended way): setting the option <code>log4jdbc.spylogdelegator.name</code> to provide the qualified class name of your implementation of <code>SpyLogDelegator</code>. See below fore more details about setting log4jdbc options. </li>
<li><strong>Option 2</strong>: using the method <code>net.sf.log4jdbc.log.SpyLogFactory.setSpyLogDelegator(SpyLogDelegator)</code> in your application. This method must be called before the loading of the log4jdbc-log4j2 driver, and thus should be called before any call to a <code>DriverManager</code> or <code>DataSource</code>. </li>
<li><strong>Option 3</strong>: using the method <code>net.sf.log4jdbc.sql.jdbcapi.DataSourceSpy.setLogDelegator(SpyLogDelegator)</code> in your application or your <code>bean</code> declaration. This method allows to use different log formatters for different data sources. Note that you still need to provide a default log formatter (used for log4jdbc initialization), either by using the default <code>SpyLogDelegator</code> for Log4j 2 (no action required besides installing Log4j 2), or by configuring through one of the first two options the <code>SpyLogDelegator</code> for SLF4J, or your own custom logger.</li>
</ul>
</p>

<br>
<br>
<hr /><br>
<br>
<br>
<br>
<h1>Configure log4jdbc-log4j2 options</h1>
log4jdbc-log4j2 can be configured in the exact same way than log4jdbc (see below). Please note two changes as compared to log4jdbc:<br>
<ul>
<li><strong><code>log4jdbc.spylogdelegator.name</code>: </strong>this is a new option, allowing to provide the qualified class name of the logger to use. Notably, if you want to use the SLF4J logger rather than Log4j 2, you must set this option to the value <strong><code>net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator</code></strong>.</li>
<li><strong><code>log4jdbc.debug.stack.prefix</code>: </strong>this property is now a REGEX, instead of being just the package prefix of the stack trace. So, for instance, if you want to target the prefix <code>org.mypackage</code>, the value of this property should be: <code>^org\.mypackage.*</code>.</li>
</ul>

<h2>Configuration file or System properties</h2>
<p>From the log4jdbc documentation: you can define any of the log4jdbc settings either from a file named <strong>log4jdbc.log4j2.properties</strong> stored in the classpath, or via System properties. log4jdbc will look for properties both in the configuration file (if it exists) and in the system properties, with the file taking precedence for any properties defined in both locations. </p>

<p>For instance, if you want to set the option <code>log4jdbc.spylogdelegator.name</code>, you can either: add to the <code>log4jdbc.log4j2.properties</code> file:<br>
<pre><code>log4jdbc.spylogdelegator.name=net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator<br>
</code></pre>
</p>
<p>Or: use System properties:<br>
<pre><code>java -Dlog4jdbc.spylogdelegator.name=net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator -classpath ./classes my.funky.Program<br>
</code></pre>
</p>

<h2>log4jdbc-log4j2 options</h2>
<table><thead><th><strong>property</strong></th><th><strong>default</strong></th><th><strong>description</strong></th></thead><tbody>
<tr><td>log4jdbc.drivers</td><td>  </td><td>One or more fully qualified class names for JDBC drivers that log4jdbc should load and wrap. If more than one driver needs to be specified here, they should be comma separated with no spaces. This option is not normally needed because most popular JDBC drivers are already loaded by default-- this should be used if one or more additional JDBC drivers that (log4jdbc doesn't already wrap) needs to be included. </td></tr>
<tr><td>log4jdbc.auto.load.popular.drivers</td><td>true</td><td>Set this to false to disable the feature where popular drivers are automatically loaded. If this is false, you must set the log4jdbc.drivers property in order to load the driver(s) you want.</td></tr>
<tr><td>log4jdbc.debug.stack.prefix</td><td>  </td><td>A REGEX matching the package name of your application. The call stack will be searched down to the first occurrence of a class that has the matching REGEX. If this is not set, the actual class that called into log4jdbc is used in the debug output (in many cases this will be a connection pool class.) For example, setting a system property such as this: <code>-Dlog4jdbc.debug.stack.prefix=^com\.mycompany\.myapp.*</code> would cause the call stack to be searched for the first call that came from code in the com.mycompany.myapp package or below, thus if all of your sql generating code was in code located in the com.mycompany.myapp package or any subpackages, this would be printed in the debug information, rather than the package name for a connection pool, object relational system, etc. <br /> <strong>Please note that the behavior of this property has changed as compared to the standard log4jdbc implementation</strong>. This property is now a REGEX, instead of being just the package prefix of the stack trace. So, for instance, if you want to target the prefix <code>org.mypackage</code>, the value of this property should be: <code>^org\.mypackage.*</code>.</td></tr>
<tr><td>log4jdbc.sqltiming.warn.threshold</td><td>  </td><td>Millisecond time value. Causes SQL that takes the number of milliseconds specified or more time to execute to be logged at the warning level in the sqltiming log. Note that the sqltiming log must be enabled at the warn log level for this feature to work. Also the logged output for this setting will log with debug information that is normally only shown when the sqltiming log is enabled at the debug level. This can help you to more quickly find slower running SQL without adding overhead or logging for normal running SQL that executes below the threshold level (if the logging level is set appropriately.) </td></tr>
<tr><td>log4jdbc.sqltiming.error.threshold </td><td>  </td><td>Millisecond time value. Causes SQL that takes the number of milliseconds specified or more time to execute to be logged at the error level in the sqltiming log. Note that the sqltiming log must be enabled at the error log level for this feature to work. Also the logged output for this setting will log with debug information that is normally only shown when the sqltiming log is enabled at the debug level. This can help you to more quickly find slower running SQL without adding overhead or logging for normal running SQL that executes below the threshold level (if the logging level is set appropriately.) </td></tr>
<tr><td>log4jdbc.dump.booleanastruefalse </td><td>false </td><td>When dumping boolean values in SQL, dump them as 'true' or 'false'. If this option is not set, they will be dumped as 1 or 0 as many databases do not have a boolean type, and this allows for more portable sql dumping. </td></tr>
<tr><td>log4jdbc.dump.sql.maxlinelength </td><td>90 </td><td>When dumping SQL, if this is greater than 0, than the dumped SQL will be broken up into lines that are no longer than this value. Set this value to 0 if you don't want log4jdbc to try and break the SQL into lines this way. In future versions of log4jdbc, this will probably default to 0. </td></tr>
<tr><td>log4jdbc.dump.fulldebugstacktrace </td><td>false </td><td>If dumping in debug mode, dump the full stack trace. This will result in EXTREMELY voluminous output, but can be very useful under some circumstances when trying to track down the call chain for generated SQL.</td></tr>
<tr><td>log4jdbc.dump.sql.select </td><td>true </td><td>Set this to false to suppress SQL select statements in the output. Note that if you use the Log4j 2 logger, it is also possible to control select statements output via the marker <code>LOG4JDBC_SELECT</code> (see section "Disabling some SQL operations, or dispatching them in different files" above). The use of this property prepend the use of the marker.</td></tr>
<tr><td>log4jdbc.dump.sql.insert </td><td>true </td><td>Set this to false to suppress SQL insert statements in the output. Note that if you use the Log4j 2 logger, it is also possible to control insert statements output via the marker <code>LOG4JDBC_INSERT</code> (see section "Disabling some SQL operations, or dispatching them in different files" above). The use of this property prepend the use of the marker.</td></tr>
<tr><td>log4jdbc.dump.sql.update </td><td>true </td><td>Set this to false to suppress SQL update statements in the output. Note that if you use the Log4j 2 logger, it is also possible to control update statements output via the marker <code>LOG4JDBC_UPDATE</code> (see section "Disabling some SQL operations, or dispatching them in different files" above). The use of this property prepend the use of the marker.</td></tr>
<tr><td>log4jdbc.dump.sql.delete </td><td>true </td><td>Set this to false to suppress SQL delete statements in the output. Note that if you use the Log4j 2 logger, it is also possible to control delete statements output via the marker <code>LOG4JDBC_DELETE</code> (see section "Disabling some SQL operations, or dispatching them in different files" above). The use of this property prepend the use of the marker.</td></tr>
<tr><td>log4jdbc.dump.sql.create </td><td>true </td><td>Set this to false to suppress SQL create statements in the output. Note that if you use the Log4j 2 logger, it is also possible to control create statements output via the marker <code>LOG4JDBC_CREATE</code> (see section "Disabling some SQL operations, or dispatching them in different files" above). The use of this property prepend the use of the marker.</td></tr>
<tr><td>log4jdbc.dump.sql.addsemicolon </td><td>false </td><td>Set this to true to add an extra semicolon to the end of SQL in the output. This can be useful when you want to generate SQL from a program with log4jdbc in order to create a script to feed back into a database to run at a later time.</td></tr>
<tr><td>log4jdbc.spylogdelegator.name</td><td>net.sf.log4jdbc.log.log4j2.Log4j2SpyLogDelegator</td><td>The qualified class name of the <code>SpyLogDelegator</code> to use. Note that if you want to use log4jdbc-log4j2 with SLF4J rather than Log4j 2, you must set this property to: <code>net.sf.log4jdbc.log.slf4j.Slf4jSpyLogDelegator</code>. This is a new property, not present in the standard log4jdbc implementation.</td></tr>
<tr><td>log4jdbc.statement.warn </td><td>false </td><td>Set this to true to display warnings (Why would you care?) in the log when Statements are used in the log. NOTE, this was always true in releases previous to 1.2alpha2. It is false by default starting with release 1.2 alpha 2. </td></tr>
<tr><td>log4jdbc.trim.sql </td><td>true </td><td>Set this to false to not trim the logged SQL. (Previous versions always trimmed the SQL.) </td></tr>
<tr><td>log4jdbc.trim.sql.extrablanklines </td><td>true </td><td>Set this to false to not trim extra blank lines in the logged SQL (by default, when more than one blank line in a row occurs, the contiguous lines are collapsed to just one blank line.) (Previous versions didn't trim extra blank lines at all.) </td></tr>
<tr><td>log4jdbc.suppress.generated.keys.exception </td><td>false </td><td>Set to true to ignore any exception produced by the method, Statement.getGeneratedKeys() (Useful for using log4jdbc with Coldfusion </td></tr></tbody></table>

Of note, an additional property allows to set the name of the property file:<br>
<table><thead><th><strong>property</strong></th><th><strong>default</strong></th><th><strong>description</strong></th></thead><tbody>
<tr><td>log4jdbc.log4j2.properties.file </td><td>log4jdbc.log4j2.properties </td><td>Set the name of the property file to use </td></tr></tbody></table>

<br>
<br>
<hr /><br>
<br>
<br>
<br>
<h1>Slight modifications as compared to the standard implementation</h1>
<ul>
<li><strong>connection opening</strong>: if the log4jdbc Driver is used to acquire the connection to the database, the execution time to open the connection is now logged. This is not the case if the connection is opened directly in your code as explained in the <a href='http://code.google.com/p/log4jdbc/' title='External link to log4jdbc'>log4jdbc FAQ</a>. However, new constructors for <code>ConnectionSpy</code> have been added, allowing to provide this execution time for logging.</li>
<li><strong>connection closing</strong>: time to close the connection is now always logged.</li>
<li><strong>connection number for statements: </strong>: in log4jdbc, SQL connection number information is generated to help identify connection pooling or threading problems. This connection number was not displayed for logging of SQL statements, now it is.</li>
<li><strong>logging of <code>getGeneratedKeys()</code>: </strong>calls to <code>getGeneratedKeys()</code> were not logged as standard SQL statements, but only as an <code>audit</code> information (through the use of the logger <code>jdbc.audit</code>). They are now properly logged, along with the SQL statement on which they were performed. </li>
<li>Minor changes in line returns or logs presentation. This might break the scripts provided by log4jdbc to parse the logs.</li>
</ul>
<br>
<br>
<hr /><br>
<br>
<br>
<br>
<h1>To do</h1>
<ul>
<li>Maybe use the <code>entry()</code> and <code>exit()</code> methods of Log4j 2, rather than the <code>methodReturned()</code> of the <code>SpyLogDelegator</code>.</li>
</ul>