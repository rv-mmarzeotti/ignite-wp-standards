# Ignite WordPress Standards

Some basic standards to avoid conflicts with modules used in different order and on different pages.

## Padding, Margins and Borders

Padding, margins and borders should be kept to the bottom and right when used to create space between elements. The exception to this rule is if the module has a background color or image and needs padding on the top to match the design. This ensures that stacked modules have the correct spacing between them and could be placed in any order. Often times our modules will have transparent backgrounds with uniform spacing between them or very specific spacing based on the individual module. Complete buy in on the team will ensure that everyone knows where padding and margin will be located no matter the implementation and can make QA edits without worrying it breaks other areas of the design.

### Examples

In a recent edit on FurnaceCompare.com, the dev team was tasked with adding a border above the "Reviews Overview" section on [product pages](https://www.furnacecompare.com/furnaces/products/trane/xv95/). Doing so exactly the way the request was posed would cause a double border on [brand pages](https://www.furnacecompare.com/furnaces/products/trane/) that also use the same "Reviews Overview" module. Buy in on borders only on the bottom of elements would prevent that from happening even if the developer making the change was unaware of the use of the module on brand pages.

#### Product Pages

![Product Pages](/images/example-1-1.png)

#### Brand Pages

![Brand Pages](/images/example-1-2.png)