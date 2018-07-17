# Responsive Typography

## Fluid Type in conjunction with Modular Scale

It is possible to have precise control over responsive typography. Using calc() and viewport units you can create fluid type that scales perfectly between specific pixel values, within a specific viewport range.

You need this boilerplate for responsive typography in your projects, work with headings, paragraphs and vertical balance. Supplied with some parameters try to figured out what is your perfect basic setup. 


## What's inside? 

- Basic Settings: $fontSize-min, $fontSize-max, $lineHeight-base
- Type Scale Settings: $Width-min, $Width-max, $scaleFactor, $baseline
- Type Scale Chart

I've renounced a Font Map. The magic happens in the mixin.scss ;)


	@mixin fluid-type($properties, $min-vw, $max-vw, $min-value, $max-value) {
	  @each $property in $properties {
	    #{$property}: $min-value;
	  }

	  @media screen and (min-width: $min-vw) {
	    @each $property in $properties {
	      #{$property}: calc(#{$min-value} + #{strip-unit($max-value - $min-value)} * (100vw - #{$min-vw}) / #{strip-unit($max-vw - $min-vw)});
	    }
	  }

	  @media screen and (min-width: $max-vw) {
	    @each $property in $properties {
	      #{$property}: $max-value;
	    }
	  }
	}

	@function strip-unit($value) {
	  @return $value / ($value * 0 + 1);
	}


Change the parameters for your own setup that you want.


## Credits
- [Mike Mike Riethmuller](https://www.madebymike.com.au/writing/fluid-type-calc-examples/) - for some inspiration
- [Hugo Giraudel & Eduardo Bouças](http://include-media.com/) - for Sass media

