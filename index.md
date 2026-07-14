
# Project Portfolio


A nursery professional, statistician, and digital mapper seeking to combine the best of all worlds. 

Below are some of my projects highlighing skillsets that include digital map-making, data integration, data analysis, coding, and quantitative reasoning

## Digital Mapping

One of the benefits of a digital map is the ability to transform space into a database for intuitive information retrieval. Especially in the field of horticulture, knowing where plants are rooted or temporarily placed opens the door to questions about access, plant interaction, symbiosis. An a list of plants and their attributes just won't do. The projects below were started while earning an Associates degree in Geographical Information Systems (GIS) at Chabot College. 

```
Map of Nursery
```
One of the most frequently asked questions at my nursery is "where is x plant?" I created a digital map of the nursery so that customers and staff can address questions like these.


![digital map of plant nursery](assets/img/nursery_map/full_map.png)
![digital map of plant nursery](assets/img/nursery_map/native_popup.png)
![digital map of plant nursery](assets/img/nursery_map/goldenCurrant.png)
```
Park Tree Inventory 
```
![digital map of park assests](assets/img/hayward_park_pics/pic3.png)
![digital map of park assests](assets/img/hayward_park_pics/pic1.png)
![digital map of park assests](assets/img/hayward_park_pics/pic2.png)


## Coding 
```
Visualizing Geometric Symmetries
```
While completing a Master degree in Statistics at San Francisco State Universtiy, I took an Abstract Algebra course. I learned that, like the integers or real numbers, shapes have multiplication tables too. These multiplication tables can look even more abstract than a 12x12 times table, with letters and numbers corresponding to a rotation or reflection of an underlying shape. I wondered what a square's multiplication talbe looked like with color. I computed the multiplication tables of squares, hexagons, and rectangles in <a href="https://github.com/Akunwa/portfolio2/blob/main/assets/doc/vis_geom_sym.ipynb" target="_blank" rel="noreferrer noopener">Python</a>, then applied heat maps to these tables to reveal their symmetries.

![visualizing geometric symmetries](assets/img/visGeomSym.png)

<details>
<summary>Click to expand code</summary>

```python
def hello_world():
    print("Hello, World!")
```

</details>

the symmetries of a polygon can be formulated as the transformations that maintain sameness of the shape. For instance, a square's symmetries are the rotations and reflections of the shape that look the same as a non-rotated, non-reflected square. The set of all rotations and reflections that maintain the sameness of a shape forms an Algebraic Group, a mathematical formulation where arithmetic can be applied. One of the best known groups is the set of all positive and negative integers. All algebraic groups have multiplication tables which can be computed by composing elements of the Group with each other i.e a reflection of a square followed by a rotation. 
