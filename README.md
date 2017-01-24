# hello-world
this is a learning project


// Backbone Model

var Book = Backbone.Model.extend({
	defaults: {
		book: '',
		author: '',
		price: ''
	}


// instantiate 2 models

var book1 = new Book({
	book: 'A Bend in the River',
	author: 'V. S. Naipaul',
	price: '100'
});


var book3 = new Book({
	book: '22 Days in India',
	author: 'Anurag Mathur',
	price: '50'
});


// instantiate a Collection

var books = new Books([book1,book2,book3]);

// Backbone View for one book

var BookView = Backbone.View.extend({
	model: new Book(),
	tagName: 'tr',
	initialize: function() {
		this.template = _.template($('.book-list-template').html());
		console.log("template called");
	},
	events: {
		'click .edit-book': 'edit',
		'click .update-book': 'update',
		'click .cancel': 'cancel',
		'click .delete-book': 'delete'
		
	},
	 
	edit: function() {
		$('.edit-book').hide();
		$('.delete-book').hide();
		this.$('.update-book').show();
		this.$('.cancel').show();

		var book = this.$('.book').html();
		var author = this.$('.author').html();
		var price = this.$('.price').html();
 
		this.$('.book').html('<input type="text" class="form-control book-update" value="' + book + '">');
		this.$('.author').html('<input type="text" class="form-control author-update" value="' + author + '">');
		this.$('.price').html('<input type="text" class="form-control price-update" value="' + price + '">');
	},
	update: function() {
		this.model.set('book', $('.book-update').val());
		this.model.set('author', $('.author-update').val());
		this.model.set('price', $('.price-update').val());
	},
	cancel: function() {
		booksView.render();
	},
	delete: function() {
		this.model.destroy();
	},
	this sis somethin g thatcan be rendered using backbone layout manager
	
});

// Backbone View for collection

var BooksView = Backbone.View.extend({
	model: books,
	el: $('.catalogue'),
	initialize: function() {
		var self = this;
		this.model.on('add', this.render, this);
		this.model.on('change', function() {
			setTimeout(function() {
				self.render();
			}, 30);
		},this);
	
		this.model.on('remove', this.render, this);
	},
	render: function() {
		var self = this;
		this.$el.html('');
		
		_.each(this.model.toArray(), function(book) {
			
			self.$el.append((new BookView({model: book})).render().$el);
		});
		return this;
	}
});


var booksView = new BooksView();

$(document).ready(function() {
	booksView.render();
		booksView.render();
			booksView.render();
				booksView.render();
	$('.add-input').on('click', function() {
		var bookNew = new Book({
			book: $('.book-input').val(),
			author: $('.author-input').val(),
			price: $('.price-input').val()
		});
		$('.book-input').val('');
		$('.author-input').val('');
		$('.price-input').val('');
		console.log(bookNew.toJSON());
		books.add(bookNew);
	})

})
