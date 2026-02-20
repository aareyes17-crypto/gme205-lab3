# GmE 205 Laboratory 3: Spatial Object Systems
# How to set up the virtual environment
# How to run Python scripts

# B.5 Conceptual Reflection
- What changed in the internal representation of Point?
- The Point class no longer stores the longitude and latitude (self.lon, self.lat) as separate attributes, but as a Shapely geometry object (self.geometry) which encapsulates both the coordinate data and spatial behavior. The Coordinates are now accessed as properties of the geometry object.

- What did not change in the external behavior? 
- The public interface of the class, the method such as to_tuple() and distance_to(), as well as the expected outputs they produce, all did not change.

- Where does spatial computation now live? 
- The spatial computation now lives inside the Shapely geometry engine. Instead of manually implementing formulas, the class is now delegating spatial operations to the self.geometry object.
