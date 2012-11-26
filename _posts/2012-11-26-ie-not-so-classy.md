---
title: IE - Not so classy
layout: post
category : technology
tags : [internet explorer, javascript]
---
{% include JB/setup %}

After encountering the [Internet Explorer Trailing Comma of Death]{% post_url 2012-03-22-ie-trailing-comma-of-death %}, I ran into some more IE troubles while working on a different site. As can be expected, everything was running fine on Firefox and Chrome. But the site (mainly built with javascript) just die in IE? The error message was similar to the Trailing Comma of Death error message, so I started scanning the code for trailing comma''s. 

I didn''t find any right away, so I installed jslint and ran that. Unfortunately jslint generates a lot of errors for things that aren''t really that big of a deal (indentation mainly), so real errors get rather lost in a flood of message saying that it was expecting line X to start at position Y in stead of Z. Not that helpfull. But I did go through all the files and fixed everything that looked more or less like a possible error. But sill the damned thing wouldn''t run in IE (8 by the way).

So, I turned to my old friend google and started looking for other reasons for that particular error message. And so it turns out that this time the culprit was the **class** keyword. Turns out I had the following in my code:

	var locatie_kiezer = new FilteringSelect({
		store: this.store,
		name: 'locatie_kiezer',
		placeholder: 'Geef een gemeente, straat of adres op.',
		searchAttr: 'locatie',
		labelAttr: 'id',
		hasDownArrow: false,
		class: 'locatieKiezer'
	});

Works fine in Firefox, Chrome (and probably Safari), but not in IE 8 because class is a reserved keyword. Once I figured what the problem was, the solution was actually quite simple: just put the key in quotes:

	var locatie_kiezer = new FilteringSelect({
		store: this.store,
		name: 'locatie_kiezer',
		placeholder: 'Geef een gemeente, straat of adres op.',
		searchAttr: 'locatie',
		labelAttr: 'id',
		hasDownArrow: false,
		'class': 'locatieKiezer'
	});

Kind of curious, what it''ll be next time.
