# # ["doesn't declare an explicit app_label"](https://stackoverflow.com/questions/40206569/django-model-doesnt-declare-an-explicit-app-label)
This error usually happens when project file names coincide with file names of imported modules. For example, if you have models.py file, and you import django library, which implicitly has a models.py file

Solution: be explicit when importing these files, so if you want to import the project's models.py which is inside a folder called my_project, then import it like this `import my_project.models` instead of `import models` ([source](https://stackoverflow.com/questions/40206569/django-model-doesnt-declare-an-explicit-app-label#:~:text=I%20got%20this%20error,Hope%20this%20helps!))
