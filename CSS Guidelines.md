# CSS : notes, conseils, indications
**[Follow me on Twitter](http://twitter.com/csswizardry) and [tweet these guidelines](https://twitter.com/intent/tweet?text=CSS+Guidelines+by+%40csswizardry%3A+https://github.com/csswizardry/CSS-Guidelines/).**


## Documents CSS

Nous maintenons une table des matières en haut de chaque fichier CSS. Celle-ci indique les sections dans le document.
Chacune d'elles est préfixée avec un symbole `$`. Ainsi, une recherche pour `$[nom de la section]` ne donnera que des résultats qui sont des sections.

### Syntaxe et formatage
Nous utilisons du CSS multi-ligne pour simplifier le contrôle de version (c'est un cauchemar d'effectuer un diff sur du CSS mono-ligne), et nous trions les déclarations CSS par pertinence… **pas** alphabétiquement.

Nous utilisons des sélecteurs limités par des tirets, en minuscules : `.pasBien{}`, `.pas_bien_non_plus{}` mais `.celui-ci-est-bien{}`.

Toujours laisser un dernier point-virgule après la dernière déclaration d'un ruleset, pour éviter toute confusion ou erreur de syntaxe au cours de la vie du document.

Pour avoir un exemple de la structure et du formatage que nous privilégions dans nos fichiers CSS, jetez un œil à [github.com/csswizardry/vanilla/&hellip;/style.css](http://github.com/csswizardry/vanilla/blob/master/css/style.css).

**À lire :**

* [coding.smashingmagazine.com/&hellip;/writing-css-for-others](http://coding.smashingmagazine.com/2011/08/26/writing-css-for-others)
* [jasoncale.com/&hellip;/5-dont-format-your-css-onto-one-line](http://jasoncale.com/articles/5-dont-format-your-css-onto-one-line)


## Commentaires

Commentez autant que possible, aussi souvent que possible. Là où ça pourrait être utile, incluez un petit bout de HTML en commentaire pour aider à situer le CSS dans son contexte.

Soyez bavard ! Lâchez-vous ! Le CSS sera minifié avant d'atteindre les serveurs de prod, de toute façon.


## Indentation

Pour chaque niveau de profondeur dans le HTML, essayez d'indenter votre CSS pour coller au mieux. Par exemple :

    .nav{}
        .nav li{}
            .nav a{}
            
    .promo{}
        .promo p{}


Et aussi, écrivez vos déclarations avec préfixes navigateurs de sorte à aligner les double-points, comme ceci :

    -webkit-border-radius:4px;
       -moz-border-radius:4px;
            border-radius:4px;

Ainsi, on peut parcourir la feuille de style en diagonale et voir qu'ils sont tous réglés sur 4 pixels, mais plus important : si votre éditeur le permet, vous pouvez taper en colonnes pour tous les changer d'un coup.

## Ajouter des composants

Si vous construisez un nouveau composant, écrivez le HTML **avant** le CSS. Ainsi, vous pourrez visualiser quelles propriétés CSS sont hérités naturellement, et éviter de réappliquer des styles redondants.


## CSS orienté objet

En concevant vos composants, essayez de garder à l'esprit une structure de type DRY (don't repeat yourself) et orientée objet.

Au lieu de construire des douzaines de composants indépendants, essayez de repérer les motifs qui se répètent ; construisez ces squelettes comme des « objets » de base, et ajoutez-leur des classes pour adapter leur apparence à leurs spécificités.

Si vous avez un nouveau composant à construire, séparez-en la structure et l'apparence ; construisez la structure du composant à l'aide de classes très génériques. Ainsi, il sera possible de réutiliser le « constructeur » et d'ajouter un design spécifique ensuite.

**À lire :**

* [csswizardry.com/&hellip;/the-nav-abstraction](http://csswizardry.com/2011/09/the-nav-abstraction)
* [stubbornella.org/&hellip;/the-media-object-saves-hundreds-of-lines-of-code](http://stubbornella.org/content/2010/06/25/the-media-object-saves-hundreds-of-lines-of-code)


## Structure générale

Tous les composants devraient être totalement dépourvus de largeur ; vos composants devraient toujours rester élastiques, leurs largeurs étant fixées par un système de grille.
All components should be left totally free of widths; your components should always remain fluid and their widths should be governed by a grid system.

Il ne faut **jamais** appliquer de hauteur aux éléments. Il ne faudrait appliquer de hauteur qu'aux choses qui avaient des dimensions _avant_ d'atterrir sur le site (les images et les sprites). Il ne faut jamais, au grand jamais, donner de hauteur aux éléments `p`, `ul`, `div`, et ainsi de suite. Normalement, vous devriez obtenir l'effet désiré avec des propriétés line-height, qui sont beaucoup plus flexibles.

Considérez les grilles comme des étagères. Elles contiennent du contenu, mais ne sont pas du contenu elles-mêmes. Vous assemblez vos étagères, ensuite vous les remplissez de trucs.

Vous ne devriez jamais appliquer de style sur un élément de grille : ils sont là uniquement à des fins de mise en page. Quelles que soient les circonstances, n'appliquez jamais de propriété de type box-model à un élément de grille.


## Dimensionnement

Nous utilisons une combinaison de plusieurs méthodes pour dimensionner les interfaces. Pourcentages, pixels, ems, rems et rien du tout.

**À lire :**

* [csswizardry.com/&hellip;/measuring-and-sizing-uis-2011-style](http://csswizardry.com/2011/12/measuring-and-sizing-uis-2011-style)


## Tailles des polices

Nous utilisons des rems (avec un fallback en pixels, pour les plus vieux navigateurs seulement). Il n'est pas question de définir une taille de police en pixels par défaut. Nous définissons les hauteurs de ligne sans unité, **sauf** si nous voulons aligner le texte avec des hauteurs connues.

Nous voulons éviter de définir les tailles de police encore et encore. Pour y arriver, nous avons une échelle prédéfinie de tailles de polices associées à des classes. Nous les recyclons au lieu de redéclarer les propriété de taille plusieurs fois.

Avant d'ajouter une déclaration font-size, voyez si une classe pour cette taille-là n'existe pas déjà.

**Read:**

* [csswizardry.com/&hellip;/pragmatic-practical-font-sizing-in-css](http://csswizardry.com/2012/02/pragmatic-practical-font-sizing-in-css)


## Shorthand

It might be tempting to use declarations like `background:red;` but in doing so what we are actually saying is ‘I want no image to scroll, aligned top left and repeating X and Y and a background colour of red’. Nine times out of ten this won’t cause any issues but that one time it does is annoying enough to warrant not using such shorthand. Instead use `background-color:red;`.

Similarly, declarations like `margin:0;` are nice and short, but **be explicit**. If you’re actually only really wanting to affect the margin on the bottom of an element then it is more appropriate to use `margin-bottom:0;`.

Be explicit in which properties you set and take care to not inadvertently unset others with shorthand. E.g. if you only want to remove the bottom margin on an element then there is no sense in blitzing all margins with `margin:0;`.

Shorthand is good, but easily misused.


## Selectors

Keep selectors efficient and portable.

Heavily location-based selectors are bad for a number of reasons. For example, take `.sidebar h3 span{}`. This selector is too location-based and thus we cannot move that `span` outside of a `h3` outside of `.sidebar` and maintain styling.

Selectors which are too long also introduce performance issues; the more checks in a selector (e.g. `.sidebar h3 span` has three checks, `.content ul p a` has four), the more work the browser has to do.

Make sure styles aren’t dependent on location where possible, and make sure selectors are nice and short.

**Remember:** classes are neither semantic or insemantic; they are sensible or insensible! Stop stressing about ‘semantic’ class names and pick something sensible and futureproof.

**Read:**

* [speakerdeck.com/&hellip;/breaking-good-habits](http://speakerdeck.com/u/csswizardry/p/breaking-good-habits)
* [csswizardry.com/&hellip;/writing-efficient-css-selectors](http://csswizardry.com/2011/09/writing-efficient-css-selectors)

### Over-qualified selectors

An over-qualified selector is one like `div.promo`. We could probably get the same effect from just using `.promo`. Of course sometimes we will _want_ to qualify a class with an element (e.g. if you have a generic `.error` class that needs to look different when applied to different elements (e.g. `.error{ color:red; }` `div.error{ padding:14px; }`)), but generally avoid it where possible.

Another example of an over-qualified selector might be `ul.nav li a{}`. As above, we can instantly drop the `ul` and because we know `.nav` is a list, we therefore know that any `a` _must_ be in an `li`, so we can get `ul.nav li a{}` down to just `.nav a{}`.

### Performance

Whilst it is true that browsers will only ever keep getting faster at rendering CSS, efficiency is something we could do to keep an eye on. Short selectors, not using the universal (`*{}`) selector and avoiding more complex CSS3 selectors should help circumvent these problems.

**Read:**

* [csswizardry.com/…/writing-efficient-css-selectors](http://csswizardry.com/2011/09/writing-efficient-css-selectors)


## Be explicit, don’t make assumptions

Instead of using selectors to drill down the DOM to an element, it is often best to put a class on the element you explicitly want to style. Let’s take a specific example.

Imagine you have a promotional banner with a class of `.promo` and in there there is some text and call-to-action link. If there is just one `a` in the whole of `.promo` then it may be tempting to style that call-to-action via `.promo a{}`.

The problem here should be obvious in that as soon as you add a simple text link (or any other link for that matter) to the `.promo` container it will inherit the call-to-action styling, whether you want it to or not. In this case you would be best to explicitly add a class (e.g. `.cta`) to the link you want to affect.

Be explicit; target the element you want to affect, not its parent. Never assume that markup won’t change.


## IDs and classes

Do not use IDs in CSS **at all**. They can be used in your markup for JS and fragment-identifiers but use only classes for styling. We don’t want to see a single ID in this (or any other) stylesheet.

Classes come with the benefit of being reusable (even if we don’t want to, we can) and they have a nice, low specificity.

**Read:**

* [csswizardry.com/&hellip;/when-using-ids-can-be-a-pain-in-the-class](http://csswizardry.com/2011/09/when-using-ids-can-be-a-pain-in-the-class)


## `!important`

It is okay to use `!important` on helper classes only. To add `!important` preemptively is fine, e.g. `.error{ color:red!important }`, as you know you will **always** want this rule to take precedence.

Using `!important` reactively, e.g. to get yourself out of nasty specificity situations, is not advised. Rework your CSS and try to combat these issues by refactoring your selectors. Keeping your selectors short and avoiding IDs will help out here massively.


## Magic numbers and absolutes

A magic number is a number which is used because ‘it just works’. These are bad because they rarely work for any real reason and are not usually very futureproof or flexible/forgiving. They tend to fix symptoms and not problems.

For example, using `.dropdown-nav li:hover ul{ top:37px; }` to move a dropdown to the bottom of the nav on hover is bad, as 37px is a magic number. 37px only works here because in this particular scenario the `.dropdown-nav` happens to be 37px tall.

Instead we should use `.dropdown-nav li:hover ul{ top:100%; }` which means no matter how tall the `.dropdown-nav` gets, the dropdown will always sit 100% from the top.

Every time you hard code a number think twice; if you can avoid it by using keywords or ‘aliases’ (i.e. `top:100%` to mean ‘all the way from the top’) or&mdash;even better&mdash;no measurements at all then you probably should.

Every hard-coded measurement you set is a commitment you might not necessarily want to keep.


## Conditional stylesheets

IE stylesheets can, by and large, be totally avoided. The only time an IE stylesheet may be required is to circumvent blatant lack of support (e.g. PNG fixes).

As a general rule, all layout and box-model rules can and _will_ work without an IE stylesheet if you refactor and rework your CSS. This means we never want to see `<!--[if IE 7]> element{ margin-left:-9px; } < ![endif]-->` or other such CSS that is clearly using arbitrary styling to just ‘make stuff work’.


## Debugging

If you run into a CSS problem **take code away before you start adding more** in a bid to fix it. The problem exists in CSS that is already written, more CSS isn’t the right answer!

Delete chunks of markup and CSS until your problem goes away, then you can determine which part of the code the problem lies in.

It can be tempting to put an `overflow:hidden;` on something to hide the effects of a layout quirk, but overflow was probably never the problem; **fix the problem, not its symptoms.**


## Preprocessors

By following the above advice you should typically find the need for a preprocessor decreases dramatically. If you still wish to use a preprocessor then by all means do so, but only as en extension of the above, not an alternative.

For example, preprocessors’ nesting abilities often lead to overly specific and location dependent selectors. Let’s use our `. nav a{}` example again:

    .nav{
        li{
            a{}
        }
    }

Will compile to:


    .nav {}
    .nav li {}
    .nav li a {}

Whilst this is a very timid example, it does help illustrate how a lot of preprocessors’ built in ‘helpful’ aspects actually go against our ideals; `.nav li a{}` could (and should) just be `.nav a{}`.

Also, with mixins and the like, preprocessors teach you how to recognise abstractions&mdash;which is great&mdash;but not necessarily how to use them properly; there’s no point writing an abstracted mixin when you proceed to repeat it a dozen times in a stylesheet.

Be sure to know the ins-and-outs of excellent vanilla CSS and where a preprocessor can _aid_ that, not hinder or undo it. Learn the downsides of preprocessors inside-out and then fuse the best aspects of the two with the bad bits of neither.