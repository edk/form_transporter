(note this is just an outline in readme form.  there is no code yet)

# FormTransporter

Create a form, including sections and validations, and transport it to another app/database.

A form is an ordered list of labels, form fields, types and validations.  A submitted form is the answered form.


## Usage

#### Create Form

```ruby
transport_form = TransportForm.new(name: "My Required Contact Form")
transport_form.lines << Section.new(description: "Contact info")  # just a descriptive element
transport_form.lines << TFString.new(name: "first_name", required:true)
transport_form.lines << TFCheckbox.new(name: "")
...
transport_form.save
```

#### Transport the form (ship form to another system for answering)

```ruby
transport_form.serialize
```

(ship it off to another place.  perhaps via rest-api)

#### Get an Answer
``` ruby
@tf = TransportForm.deserialize
@tf.save
```

__ in a view __
```ruby
@tf.render
```

__ then in the transported form controller __
```ruby
tfa = TransportFormAnswer.new params[:form]
tfa.save # validation also happens, re-render on failures
```

#### Return Transport (ship back answer to originating system)

```ruby
tfa.serialize
```

And the answer(s) are associated with the original form.

