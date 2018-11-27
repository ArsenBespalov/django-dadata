=============================
django-dadata
=============================

Some django batteries for dadata.ru services


Quickstart
----------

Install django-dadata::

    pip install -e git+https://github.com/ArsenBespalov/django-dadata.git#egg=django-dadata

Then use it in a project::

    # forms.py
    
    import dadata.widgets import DadataOrgWidget
    ...
    
    # form class definition
    name = CharField(widget=DadataOrgWidget('data-linked-fields': {'inn' : '#id_vatin',
                                                                   'kpp' : '#id_reason_code'},
                                                            }))
                                                            
    # form.html
    
    # do not forget to add widget's media
    <head>
    	{{ form.media.js }}
    	{{ form.media.css }}
    </head>

How to use in admin::

    # admin.py
    from dadata.widgets import DadataAddressWidget
    
    class DaDataForm(forms.ModelForm):
        class Meta:
            model = Address
            widgets = {
                'address': DadataAddressWidget(attrs={
                    "data-linked-fields": {
                        "lat": "#id_lat",
                        "lon": "#id_lon"
                    }
                })
            }
            fields = '__all__'
            
    class AddressAdmin(admin.ModelAdmin):
        form = DaDataForm
        
    admin.site.register(Address, AddressAdmin)


Features
--------

 * Fields and validators (TODO)
 * Widgets
 	DadataOrgWidget uses dadata jquery suggestion plugin
 * REST API helpers (TODO)

Cookiecutter Tools Used in Making This Package
----------------------------------------------

*  cookiecutter
*  cookiecutter-djangopackage
