# Using Ternary Operators in Razor #

## Ternary Operators ##
Using a ternary operator is especially useful if you want to output attributes for an HTML element. It saves from using an "If" statement that breaks up the markup. The ternary operator is also useful when you want to output an HTML element that is not-self closing (Razor doesn't like having elements open, but not close, in the same code block.

### How the Ternary Operator Works ###
If your experience is in DWT design or pure front-ent, you'll probably want to know how it works. It's the same as in JavaScript and PHP:
```
 var foo = [logic statement] ? [ If True] : [ if False]; 
```

In Razor, we can run a basic ternary operation without assigning it to a variable:
```
@([logic statment] ? [If True] : [ if False] )
```

### Ternary Operator for attributes ###
This would do a basic check for a field, and if it exists, output it. If we don't have a secondary action (which is possible when just outputting text), you can just use String.Empty to finish the operation:
```
<img src="@Fields.Image" alt="@(Fields.AltText != null ? Fields.AltText : String.Empty")" />
```
This is by far the most simple, but the downside is that you could end up with a blank alt:
```
<img src="foo" alt="" />
```
If the client isn't ok with a blank "alt", then you could try this. In this case, you're putting the "alt" statement as a string, concatenating with the value, and you're escaping the quotes.
```
@(Fields.AltText != null ? "alt=\""+ Fields.AltText + " \" " : String.Empty)
```

## Adding a "First" class in a foreach loop ##
The Ternary operator is perfect when you need to add a "first" class to a list
```
	@foreach(var item in Fields.Items){
		<li  @(item.IsFirst ? "class=\"first\"" : String.Empty)>@item</li>
	}
```