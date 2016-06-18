# WPCacheManager
OSMDroid CacheManager enhanced to download map tile covered by a waypoints list.

OSMDroid CacheManager available up to 5.3, allows you to download map tiles based on a bounding box.
That's of course quite usefull as we know there are lot of places where mobile connection is not good enough to use online map.
There is a problem anyway when you develop an application providing pedestrian or cycling courses, for example, 
where the surface of the bounding box could contain lot of tiles for high zoom level whereas the tiles 
covered by the courses are finally not so many.  
The consequence is to wait a long time to donwload unusefull parts of the map.  

So this WPCacheManager, which keep the original features, add the possibility to give a list of waypoints.  
WPCacheManager considers that you will go from one waypoint to another and so will download all tiles in between.  
And as there is a possibility for your waypoint or the course to be close to the border of a tile, I decided to
download the 8 tiles around the given one at each zoom level, because I think it's not very cool to not see what's going 
few meters beside.  
Don't be afraid that's not so much, and in fact, only the first tile downloads 8 tiles more, because when you continue your trip,
some of the next 8 new tiles have already be downloaded.

# New methods:
So the new methods have been added to OSMDroid CacheManager. All added methods take care of the extra tiles downloaded 
around the GePoints list. So the method `extendedBoundsFromGeoPoints(geoPoints)` returns a larger area than the original `BoundingBoxE6.fromGeoPoints(geoPoints)`.

    public int possibleTilesCovered(ArrayList<GeoPoint> geoPoints, final int zoomMin, final int zoomMax);
    
    public void downloadAreaAsync(Context ctx, ArrayList<GeoPoint> geoPoints, final int zoomMin, final int zoomMax);
    
    public void downloadAreaAsync(Context ctx, ArrayList<GeoPoint> geoPoints, final int zoomMin, final int zoomMax, final CacheManagerCallback callback);
    
    public void downloadAreaAsyncNoUI(Context ctx, ArrayList<GeoPoint> geoPoints, final int zoomMin, final int zoomMax, final CacheManagerCallback callback);

    public void cleanAreaAsync(Context ctx, ArrayList<GeoPoint> geoPoints, int zoomMin, int zoomMax);
    
    public BoundingBoxE6 extendedBoundsFromGeoPoints(ArrayList<GeoPoint> geoPoints);
    
