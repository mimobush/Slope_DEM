# Slope_DEM
var palettes = require('users/gena/packages:palettes');

var dataset = ee.Image('USGS/SRTMGL1_003').clip(ROI);

var elevation = dataset.select('elevation');

var slope = ee.Terrain.slope(elevation);

var style = palettes.niccoli.cubicyf[7]

Map.addLayer(elevation, imageVisParam, 'elevation');

Map.addLayer(slope, {min: -11, max: 25, palette: style}, 'slope');

 Export.image.toDrive({
  image: dataset,
  description: 'Slope',
  folder: 'Slope',
  region: ROI,
  scale: 1000,
  crs: 'EPSG:4326',
  maxPixels: 1e10});
