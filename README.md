# SecurityConfigChecker

This is a security configuration validation tool for WSO2 products. 

In WSO2 products there are security configurations that are common to all products and specific to a product. Therefore this tool uses a <application_directory>/Common/properties/parent.xml file to hold the common configuration files and a <application_directory>/Product/properties/child.xml to hold product specific configuration files.This child.xml can be used to check configurations in a specific file. 

Specify the files containing common configurations in parent.xml inside file tags. For example 

    <file id="web.xml">
        <type>xml</type>
        <reference-path>/Common/configurations/web.xml</reference-path>
    </file>
   Here /Common/configurations/web.xml holds the common security configuration that should be included in a 'web.xml'. 
   The parent xml elements in this file should contain an attribute named 'configID' to hold a unique name for that specific    configuration. 
    
        <servlet id="bridge" configID="bridgeservlet">
        <servlet-name>bridgeservlet</servlet-name>
        <display-name>Carbon Bridge Servlet</display-name>
        <description>Carbon Bridge Servlet</description>
        <servlet-class>org.wso2.carbon.tomcat.ext.servlet.DelegationServlet</servlet-class>

        <load-on-startup>1</load-on-startup>
        </servlet>
  
Specify the files containing product specific configurations in child.xml inside file tags. For example 
    
    <file id="web.xml">
        <type>xml</type>
        <reference-path>/Product/configurations/tomcat/web.xml</reference-path>
        <product-path>/Product/package/web.xml</product-path>
        <exclude-config>bridgeservletMapping</exclude-config>
    </file>
   Here /Product/configurations/tomcat/web.xml file holds the product specifc configurations for the specific file in the        product in /Product/package/web.xml. Configurations defined in the child.xml overrides the configurations defined in          parent.xml. If there are configurations that needs be excluded from common configurations, they can be defined in            exclude-config.
   
   The exclude-paths tag can be used to define specific configurations files that are needed to be excluded from the check.
   
        <exclude-paths>
        <exclude-path>/Product/package/carbon/web.xml</exclude-path>
        </exclude-paths>
     
 ## Build from the source
- Get a clone or download source from [github](https://github.com/kasundharmadasa/SecurityConfigChecker)
- Run the Maven command ``mvn clean install`` from the application root directory
- Execute run.sh with the path of the product package that needs to checked as a parameter

  For example
  ``./run.sh -p <product_home>``
        
