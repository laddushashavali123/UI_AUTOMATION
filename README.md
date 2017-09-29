# ui-automation
a java base ui automation framework supporting cucumber/rest-assured/concordian, with pretty reporting as well
ui-automation is an automation BDD testing framework/solution based on cucumber-jvm, java. It provides the following features:

1.  **ability to be executed parallel up to multi-threads after easy configuration.**
2.  **rerun function is integrated with team city in order to deal with flaky test cases.**
3.  ****ability** to be configured via maven and team-city so no need of different branches for different testing scenarios**
4.  enhanced robust and stability due to the wrapper on both web-driver and web-element.
5.  **automatically mapping step definitions to the page of model**
6.  configurable reports on different format: html, log, json , etc.

# Best practice when using the framework


# Tutorials

1.  how to create a POM （page object model) for a special page object
    1.  in the folder of pages, create a new java class with the naming pattern XXXPageModel (the key word "PageModel" is important to auto-mapping)
    2.  and implement the constructor as below (assuming it's TestPageModel)  

        <pre><span style="color: rgb(0,0,128);">public class</span> TestPageModel <span style="color: rgb(0,0,128);">extends</span> BasePageModel {  
        <span style="color: rgb(0,0,128);">public</span> TestPageModel(ScenarioContext scenarioContext) <span style="color: rgb(0,0,128);">throws</span> Exception {  
        <span style="color: rgb(0,0,128);">String title = "the title of the page model that you are going to create"; //if it's set to null, it's not going to check it, useful for components.</span></pre>

        <pre><span style="color: rgb(0,0,128);">super</span>(scenarioContext, title);  
            }  
        }</pre>

    3.  now it's ready to add locators and methods when necessary
    4.  tips: for one component that may be used potentially in multiple pages, it's better to put it in to a component class , rather than creating many locators/methods on a single page.  

2.  how to create a step definition page for BDD implementation and later script writing
    1.  create a new step definition file, under the convention of XXXX**PageStepsDef** (**the part of XXX should be EXACTLY the same as that in XXXPageModel**), in our case it will be TestPageStepsDef  

    2.  currently there are two mandatory steps need to be done. one is to create a default constructor, one is to override IShouldBeOnThePage() method, where we will put validation methods when necessary.  

        public class TestPageStepsDef extends BaseStepsDef {  
        public TestPageStepsDef(ScenarioContext scenarioContext) throws Throwable {  
        super(scenarioContext);  
        }

        @Override  
        public void IShouldBeOnThePage() throws Throwable {

        }  
        }

    3.  add the object of XXXPageModel in to the BaseStepsDef everytime when adding a new pom, in our case, it's TestPageModel.  

        public abstract class BaseStepsDef {

        //declare page models, everytime when adding a new page, must declare it here  
        protected TestPageModel testPageModel;

    4.  it's ready to add business steps into this file.
    5.  tips:
        1. when a common step can be reused via multiple steps, it's advised to put it in to a separate step definition file, such as CommonStepsDef  
        2.  for setup/tearUp functions, they should be also put in this common steps def file.

3.  now we can call the functions created in any step definitions in the feature files.
    1.  in intellij ,there is a plugin cucumber can facilitate using cucumber.
    2.  after having it installed, one can use gerhkin lanugage to write steps
    3.  the IDE will suggest there is no function linked to this step. follow the instructions and choose the correct stepsDef file to put the newly created function in.
    4.  it looks like the following  

     

    5.  now a simple cucumber project is ready to run

# How to use maven to run the project
 

# How to implement rerun testing methodology via TeamCity
 
