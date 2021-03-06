# TFRS
Transportation Fuels Reporting System

### Usage
This software is being developed to streamline compliance reporting for transportation fuel suppliers  

### Data
Documentation for system data is dynamical generated using Schema Spy:
http://schema-spy-mem-tfrs-dev.pathfinder.gov.bc.ca/index.html

### Code
- css and js libraries provided as part of the Gov 2.0 Bootstrap Skeleton
- Django/Python

### Project Status
This project is in development. 
The following Deliverable have been produced:
- low-fidelity and hi-fidelity mockups for
	* Credit Transfer and Credit Awards
		- Dashboard
		- Credit account balance
		- Account activity
		- Setting, Alerts, Notifications
		- Create/Edit a proposed credit transfer
		- Accept/Approve a proposed/authorized credit transfer
	* Compliance Reporting
		- Compliance Report
		- Exclusions Report
		- Exemption Report
- prototype of credit transfer and award application using Django Templates and Static Controllers to input test data
- Deployment pipeline built out so far includes:
	* build (openshift pipeline/jenkins)
	* deploy (openshift pipeline/jenkins)
	* automated datamodeling (schema spy)
	* functional testing (navUnit) (*in progress*)
	* code analysis and vulnerability testing (sonar cubes) (*in progress*) 
- architectural deployment (*in progress*)
	* React front-end
	* REST API
	* Django Back-end
	* Postgres Database

### Development

If using Windows as your development environment, install the following:
- Python 3.5.1
- Postgresql.  Be sure to add the postgresql bin folder to your path or else you will have problems with psycopg2 not being able to find the postgrsql libraries.
- Visual Studio 2017 Community Preview with the Python extensions (As of 2017-4-18 the Preview version is required in order to use the Python extensions, which can be selected at time of install)

### Code Generation

This project has made use of the Swagger.io Code Generator.  Here is the procedure for generation of code:

1. First install an environment capable of running Java 7+ programs.  As of 2017-5-2 the current JRE can be used.   
2. If building the code generator from source, follow the instructions at the code generator extension repository:  https://github.com/bcgov/Swagger-Codegen-Extension
	1. An alternative to building from source is to obtain the jar files for the code generator and extension.
3. Make changes to the Excel file currently located at `tfrs\APISpec\in\TFRSSwagger.xlsm`
4. Export from Excel using the CTRL-SHIFT-V macro in the above excel file
5. Run the file called `update.bat` located in `tfrs\APISpec`
6. In the Swagger-Codgen-Extension folder, run the Django generator batch file with the following parameters:
7. `generate-all-django.bat <path to OpenAPI YAML file> <output folder name> <path to configuration file>
	1. The OpenAPI YAML file is located in this repository at `tfrs/ApiSpec/TFRSswagger.yaml` 
	2. The configuration file is located in this repository at `tfrs/ApiSpec/swagger-codegen-config.json`
8. Copy the following artifacts to the folder `server` in this repository.
	1. admin.py
	2. serializers.py
	3. urls.py
	4. test_api_simple
	5. views.py
	6. fakedata.py
	7. models folder
8. If the data model was changed, use the makemigrations feature of python django to make a migration (Visual Studio has a short cut to this - right click the project, select python, then Django Make Migrations...)
9. Run the migration (There is an option to run migrations in the same python menu as above)
10. Run automated tests and ensure they all pass
	1. The Visual Studio Test Explorer can be used to easily start the tests
11. Run the following to ensure code coverage works:
	1. `coverage run --source='.' manage.py test`
    2. `coverage xml`
12. Commit the code to your fork of the repository
13. Do a test build in your OpenShift instance to ensure the build works
14. If the build works, do a pull request.   


### Getting Help or Reporting an Issue
To report bugs/issues/features requests, please file an [issue](https://github.com/bcgov/tfrs/issues/).

### How to Contribute
If you would like to contribute, please see our [contributing](contributing.md) guidelines.

Please note that this project is released with a [Contributor Code of Conduct](code_of_conduct.md). By participating in this project you agree to abide by its terms.

### Licence
	Copyright 2017 Province of British Columbia

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at 

       http://www.apache.org/licenses/LICENSE-2.0

    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.

This repository is maintained by [Low Carbon Fuels Branch](http://www2.gov.bc.ca/gov/content/industry/electricity-alternative-energy/transportation-energies/renewable-low-carbon-fuels). Click [here](https://github.com/bcgov/tfrs) for a complete list of our repositories on GitHub.
