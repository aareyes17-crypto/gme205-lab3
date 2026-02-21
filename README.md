# GmE 205 Laboratory 3: Spatial Object Systems
# How to set up the virtual environment
# How to run Python scripts

# B.5 Conceptual Reflection
- What changed in the internal representation of Point?
- The Point class no longer stores the longitude and latitude (self.lon, self.lat) as separate attributes, but as a Shapely geometry object (self.geometry). The Coordinates are now accessed as properties of the geometry object.

- What did not change in the external behavior? 
- The public interface of the class, the method such as to_tuple() and distance_to(), as well as the expected outputs they produce, all did not change.

- Where does spatial computation now live? 
- The spatial computation now lives inside the Shapely geometry engine. Instead of manually implementing formulas, the class is now delegating spatial operations to the self.geometry object.

# C.6 Conceptual Reflection
- Why is SpatialObject considered an abstraction, and what real-world idea does it represent in your system?
- SpatialObject is considered an abstraction because it represents the concept that anything exists in space without defining what it specifically is. In the real world, it represents any spatial entity such as a parcel, building, or road that has geometry and spatial properties.

- How does inheritance reduce duplication between classes like Point, Parcel, or Building?
- Inheritance allows common logic, such as calculating a bounding box or checking for intersections to be written once in the parent class. The subclasses then automatically inherit all the functionality, eliminating the need to rewrite the same logic per class.

- Why is storing parcel attributes in a dictionary a structural decision rather than a behavioral one?
- Storing parcel attributes in a dictionary is structural because it defines what the object contains, instead of what the object does. The dictionary organizes and structures the attribute data, but it does not define how the object behaves, or its method. 

- If you add a new method (e.g., distance_to()) in SpatialObject, what happens to all subclasses — and why?
- If you add a new method in SpatialObject all subclasses automatically inherit the new method because they extend the base class. This is because of inheritance, since a Point is a SpatialObject, it automatically inherits all traits and behaviors defined in the parent's scope.

- How does this hierarchical design make your spatial system more scalable compared to defining each class independently?
- The hierarchical design allows new spatial types to be added easily with minimal code by inheriting from the SpatialObject. Since shared behavior is reused, redundancy is reduced and consistency is ensured, making it easier to maintain. 

# Reflection — Challenge Exercises
# Challenge 1 — from_dict() (Data → Object Boundary)
- Why should from_dict() delegate validation to the constructor instead of validating manually inside the method?
- The from_dict() should be delegating validation to the constructor because it ensures a Single Source of truth for validation logic. If the coordinate rules change, you will only need to update the constructor, and from_dict() will automatically follow the rules without needing to manually change the codes.

# Challenge 2 — as_dict() (Structured Output)
- Why is as_dict() implemented inside the object rather than in demo.py or run_lab3.py?
- The as_dict() implemented inside the object rather than in demo.py or run_lab3.py because this follows the principle of Encapsulation, where an object is responsible for managing its own data and state. Implementing it internally means that any script that uses the class can consistently export the data without having to rewrite the formatting.

- Why must as_dict() return only primitive data types and not Shapely geometry objects?
- The as_dict() must return only primitive data types and not Shapely geometry objects because the primitive types like the strings, numbers, and tuples ensures the data is "JSON-ready". 

# Challenge 3 — intersects() in SpatialObject (Inheritance)
- Why does intersects() belong in the base class instead of being duplicated in Point and Parcel?
- The intersects() belongs in the base class instead of being duplicated in Point and Parcel because it follows a Don't Repeat Yourself principle. Since the logic for intersection is identical for all the spatial objects using Shapely, defining it once in the parent class reduces the process, because there is no code duplication. 

- If you add a new spatial subclass tomorrow (e.g., Building), what changes are required for it to support intersects() — and why?
- If you add a new spatial subclass tomorrow (e.g., Building), there will be no changes required for the intersects() method. This is because the Building class simply needs to inherit from the SpatialObject. Because of Inheritance, the new class automatically gains all behaviors defined in the base class.