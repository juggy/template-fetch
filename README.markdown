Template Fetch
==============

What is it?
-----------

Template fetch retrieves a template form the server to be processed in a javascript templating engine. For now it works only with HAML (as that is my only need right now), but could be adapted to work with any other engine.

How does it work?
-----------------

You first need to load jQuery, underscore.js, haml.js and template.js.

It will fetch the template a views folder on the root of your public web directory.

To use fetch and render the template:
  
    var template_vars = { id:"1", name:"foo" };
    var callback = function( html ){ $("body").append( html ) };
    T("edit-template", template_vars, callback );
    
Remember the template is loaded using an async ajax call and stored for future uses, so your callback might be called immediately or in once the ajax call completes.

To help with this async nature, you can provide a context on which the callback ill be bound before being called:
  
  window.EditView = BaseForm.extend({
		render: function(){
			this.el.empty();
			T( "edit-template", {job : this.model.toJSON()},
					function(html){
						this.el.html(html);
					},
					this
				);
		}
	};
	

