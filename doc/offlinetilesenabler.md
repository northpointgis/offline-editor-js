API Doc for offlineTilesEnabler
===============================

##offlineTilesEnabler
Extends and overrides a tiled map service. Provides the ability to customize the extent used to cut the tiles. See the detailed description of basemap.prepareForOffline() in the "How To Use" section below to learn different options.

###Constructor
Constructor | Description
--- | ---
`OfflineTilesEnabler()` | Creates an instance of the offlineTilesEnabler class. This library allows you to extend an ArcGISTiledMapServiceLayer with offline capability as well as manage the online/offline resynchronization process.


###Methods
Methods | Returns | Description
--- | --- | ---
`extend(layer, callback)`|`callback(boolean, string)` |Overrides an ArcGISTiledMapServiceLayer. Callback is called after indexedDb store is initialized and informs the application whether it is indexedDb is supported or not.

###Properties
Property  | Description
--- | ---
`layer.offline.proxyPath`| For CORS enabled servers this can be set to `null`. The default is to use the internal resource-proxy path: `libs/offline-editor-js/resource-proxy/proxy.php.` Don't forget to check your proxy configuration to allow connections for all possible services that you might be using. More information on using proxies with ArcGIS can be found here: [https://developers.arcgis.com/javascript/jshelp/ags_proxy.html](https://developers.arcgis.com/javascript/jshelp/ags_proxy.html).

###ArcGISTiledMapServiceLayer Overrides

Methods | Returns | Description
--- | --- | ---
`getTileUrl(level, row, col)` | Url | Use the tile url's level, row and column. Retrieves tiles as requested by the ArcGIS API for JavaScript. If a tile is in cache it is returned. If it is not in cache then one is retrieved over the internet. 
`goOffline()` | nothing | This method puts the layer in offline mode. When in offline mode, the layer will not fetch any tile from the remote server. It will look up the tiles in the indexed db database and display them in the layer. If the tile can't be found in the local database it will show up blank (even if there is actual connectivity). The pair of methods `goOffline()` and `goOnline() `allows the developer to manually control the behaviour of the layer. Used in conjunction with the offline dectection library, you can put the layer in the appropriate mode when the offline condition changes.
`goOnline()` | nothing | This method puts the layer in online mode. When in online mode, the layer will behave as regular layers, fetching all tiles from the remote server. If there is no internet connectivity the tiles may appear thanks to the browsers cache, but no attempt will be made to look up tiles in the local database.
`getLevelEstimation(extent,` `level, tileSize)` | {level, tileCount, sizeBytes} | Returns an object that contains the number of tiles that would need to be downloaded for the specified extent and zoom level, and the estimated byte size of such tiles. This method is useful to give the user an indication of the required time and space before launching the actual download operation. The byte size estimation is very rough.
`getExtentBuffer(buffer,extent)`| Extent | Returns a new extent buffered by a given measurement that's based on map units. For example, if you are using mercator map projection then the buffer property would be in meters and the new extent would be returned in mercactor.
`getTileUrlsByExtent(extent, level)` | Array | Returns an array of tile urls within a given map extent and zoom level.
`deleteAllTiles(callback)` | `callback(boolean, errors)` | Clears the local cache of tiles.
`getOfflineUsage(callback)` | `callback(size, error)` | Gets the size in bytes of the local tile cache.
`getTilePolygons(callback)` | `callback(polygon, error)` | Gets polygons representing all cached tiles. This is helpful to give users a visual feedback of the current content of the tile cache.
`saveToFile(filename, callback)` | `callback( boolean, error)` | Saves tile cache into a portable csv format.
`loadFromFile(filename, callback)` | `callback( boolean, error)` | Reads a csv file into local tile cache.
`estimateTileSize(callback)` | `callback(number)` | Retrieves one tile from a layer and then returns its size.
`prepareForOffline(` `minLevel, maxLevel, extent,  ` `reportProgress)`  | `callback(number)` | Retrieves tiles and stores them in the local cache. See the "How To Use" section below to learn more about customizing the use of this method.

