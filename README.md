# ecommerce-izuchi

## Demonstration Video
<a href="https://drive.google.com/file/d/1ByWWa70pxLDgtROwuvuRU9PoiSO7atq-/view?usp=sharing">Click here to see a demonstration</a>

## Description
This project aims to offer the back-end of an e-commerce site, where we may store various items for sale alongside related information such as their price and stock, and relates these items by categories and tags to facilitate finding them. This project demonstrates the basics of how retail sites may store and associate items for sale. This way, users are able to get all related information (to potentially find items not before considered or to otherwise offer a wide breadth of options so as to maximize the potential to find something acceptable, while not overloading the user with too much unrelated information) to optimize their shopping experience. 

This project uses Sequelize to create models for our tables and seed them with data to allow us to use JavaScript to write in MySQL. Object-relational mapping is crucial to this project, in that it is what allows us to pin certain items to each other and thus allow a potential user to find items related by what they are (categories) or what they are associated with (tags). This way, if a user looks for shirts for example, they are presented with all of our shirt products (and nothing that isn't a part of the category of "shirts"). Similarly, items are grouped together by tag, such that if our user is looking for all items under the color "red," they will find any and all items tagged "red" and no items that are not tagged "red."

First, we must establish our many-to-many relationships through our 'ProductTag' model, which takes in both an item's product id as well as its tag ids, thus linking a given product to certain tags (and therefore demonstration that our product belongs to many tags through our 'ProductTag' model), such as below:
```
Product.belongsToMany(Tag, {
  through: {
    model: ProductTag, 
    unique: false
  },
});
```
In order to display associated products with our categories and tags, we must include its model in our get routes, which will display the products associated with a given category or tag below the category or tag information, as demonstrated below.
```
try {
    const categoryData = await Category.findByPk(req.params.id, {
        include: [{ model: Product }],
    });
    res.status(200).json(categoryData);
}
```
Here, we are asynchronously getting our category by it's assigned id, and displaying the category data we get back alongside it's associated products that are assigned to that category (so long as we are able to find the category by its id and received a 200 status).

## License
This project falls under the MIT license.

## Author
Damien Armstrong can be found on: <a href="https://www.linkedin.com/in/damien-armstrong-412319138/">Linkedin</a>, <a href="https://github.com/pirosvs">Github</a>