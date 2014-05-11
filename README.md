
= FormTransporter

Create a form, including sections and validations, and transport it to another app/database.

A form is an ordered list of labels, form fields, types and validations.  A submitted form is the answered form.


== Usage

==== Create Form

```ruby
transport_form = TransportForm.new(name: "My Required Contact Form")
transport_form.lines << Section.new(description: "Contact info")  # just a descriptive element
transport_form.lines << TFString.new(name: "first_name", required:true)
transport_form.lines << TFCheckbox.new(name: "")
...
transport_form.save
```

==== Transport (ship form to another system for answering)

`transport_form.serialize`
(ship it off to another place.  perhaps via rest-api)

==== Answer
``` ruby
@tf = TransportForm.deserialize
@tf.save
```

__ in a view __
`@tf.render`

__ then in the transported form controller __
```ruby
tfa = TransportFormAnswer.new params[:form]
tfa.save # validation also happens, re-render on failures
```

==== Transport (ship back answer to originating system)

`tfa.serialize`

