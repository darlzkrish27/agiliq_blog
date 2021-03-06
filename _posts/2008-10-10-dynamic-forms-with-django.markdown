---
layout: post
title:  "Dynamic forms with Django"
date:   2008-10-10 19:46:05+05:30
categories: forms
author: shabda
---
[Newforms](http://docs.djangoproject.com/en/dev/topics/forms/), (or forms now) are without doubt one of the coolest features of Django. (Of course after Admin, Localflavor, and many others). Here is some sample code.

	class EmployeeForm(forms.Form):
		name = forms.CharField()
		age = forms.IntegerField()
		resume = forms.FileField()
		
Just this code gives you 

1. A form which knows how to render itself as Html.
2. A form which knows how to validate data on the server side.
3. A form which knows how to show the relevant errors.

However think of this scenario, 

You need to customise your form depending on values in the Database.

What you want to do is 

	class EmployeeForm(forms.Form):
		name = forms.CharField()
		"Show more fields depending on the Values in DB for a specific employees."
		#....
		#....
		#....
		
You can do this without resorting to any black magic. Here is the code to do so,


	#in models.py

	type_mapping = {'CharField':forms.CharField(max_length = 100), 'TextField': forms.CharField(widget = forms.Textarea),
			'BooleanField':forms.BooleanField(required = False),
			'URLField': forms.URLField(), 'EmailField': forms.EmailField()
			}
			
	class EmployeeFieldModel(models.Model):
	    "Model for employee form fields for a specific Job board."
	    employee = models.ForeignKey(Employee)
	    name = models.CharField(max_length = 100)
	    type = models.CharField(max_length = 100)
	    order = models.IntegerField()

	#in forms.py

	def get_employee_form(employee):
	    """Return the form for a specific Board."""
	    employee_fields = EmployeeFieldModel.objects.filter(employee = employee).order_by('order')
	    class EmployeeForm(forms.Form):
		def __init__(self, *args, **kwargs):
		    forms.Form.__init__(self, *args, **kwargs)
		    self.employee = employee
		def save(self):
			"Do the save"
	    for field in employee_fields:
		setattr(EmployeeForm, field.name, copy(type_mapping[field.type]))
	    return type('EmployeeForm', (forms.Form, ), dict(EmployeeForm.__dict__))

	#in views.py

	employee = Employee.objects.get(employee_slug)
	get_employee_form(employee)


PS. A similar techniques works for Dynamic models.  
PPS. Yes I have worked with Oracle. Yes, all my data models start with Employee and Departments.

-------------

Want to build an [Web Application](http://uswaretech.com/). Talk to [Usware](http://uswaretech.com/contact/)
		


