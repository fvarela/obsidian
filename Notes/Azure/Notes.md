## Setup programing environment
VSCode extensions:
	Azure Account
	Azure Functions
	Azure Resources

Windows installs:
	Azure Functions core Tools

## Start a python function
Create the function from the terminal with:
	fun init -> start a new app
	func new -> new function in the app
	func start -> to test the new app
Create a python virtual environment with:
	python -m venv .venv
Activate virtual environment:
	./venv/Scripts/activate.bat

Test that the function runs by activating the virtual environment and running it with func start.
If everything goes ok open vscode on the folder. It will complain that the function was created outside vscode. Click ok to configure it to use with vscode. It will create a .vscode in the project.

To test VScode and debug python code:
	Run Azurite:
		F1: Azurite -> Start
		Local.setting.json:
			Should have the following line:
				"AzureWebJobsStorage": "UseDevelopmentStorage=true"
	Run debugger with F5