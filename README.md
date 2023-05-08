# Swagger API using OpenAPI Specification :bookmark_tabs:
### Open API Specification
* In .NET Core, the OpenAPI Specification (OAS), formerly known as Swagger, is a standard way to describe RESTful APIs. 
* It provides a machine-readable representation of the API's endpoints, request/response formats, authentication methods, and more. <br>
### Steps to Enable Swagger: <br>
#### Step :one:: Install the Required NuGet Packages :package:
* In ASP.NET Core project, First we need to install the Swashbuckle.AspNetCore NuGet package
* This can be done by using the Package Manager Console or the .NET CLI using the command <br>
```dotnet add package Swashbuckle.AspNetCore ```
#### Step :two:: Configure Swagger in the Startup Class
* Open the ```Startup.cs``` file in project. 
* In the ConfigureServices method, add the following code to configure Swagger
```
services.AddSwaggerGen(options =>
            {
                options.SwaggerDoc("v1",
                    new Microsoft.OpenApi.Models.OpenApiInfo
                    {
                        Title = "API Name",
                        Description = "Demo for showing swagger",
                        Version = "v1"
                    });
            });
```
* Here, AddSwaggerGen() is used to configure Swagger generation for your API. It takes an Action parameter that can be used to customize the Swagger generation behavior.
* SwaggerDoc() is used to define a Swagger document for a specific API version.
#### Step :three:: Enable Swagger Middleware
* In the Configure method of Startup.cs, add the following code to enable the Swagger middleware
```
app.UseSwagger();
app.UseSwaggerUI(c =>
{
  c.SwaggerEndpoint("/swagger/v1/swagger.json", "swagger demo api");
});
```
* Here, app.UseSwagger() will automatically generate OpenAPI documentation in a dynamic path ```swagger/v1/swagger.json```
* app.UseSwaggerUI() configures the Swagger UI (User Interface) for exploring and interacting with the OpenAPI documentation of your API.
* SwaggerEndPoint() is used to specify the location of the OpenAPI documentation file in the UI.

#### Step :four:: Add XML comments manually with a local file :writing_hand:
* First, right-click on the solution explorer and click on add new item.
* Select xml configuration file and name it as FileName.xml
* Script the XML documentation manually in FileName.xml file created above.
* Now, inject the XML file into services in Configure Services() method
```
services.AddSwaggerGen(options =>
{
    options.IncludeXmlComments("FileName.xml"); 
});
```
:triangular_flag_on_post: XML file can also be loaded from assembly using below code
```
var file = $"{Assembly.GetExecutingAssembly().GetName().Name}.xml";
var filepath=Path.Combine(AppContext.BaseDirectory, file);
options.IncludeXmlComments(filepath);
```
:sparkles: Remember!! XML should be injected from a local file in solution explorer in order to manage and update the file independently of the assembly.


#### Step :five:: Build and Run the Application:rocket:
* Build and run ASP.NET Core application. 
* Once it's running, access the Swagger UI by navigating to /swagger in web browser. 
* You should see the Swagger documentation page with the available endpoints of your API.

#### :bulb: Finally, this API documentation is used to provide a standardized and interactive way for developers to understand and consume API.
