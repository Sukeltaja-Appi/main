# Target data

[Link to Museovirasto target data](https://www.museovirasto.fi/fi/palvelut-ja-ohjeet/tietojarjestelmat/kulttuuriympariston-tietojarjestelmat/kulttuuriympaeristoen-paikkatietoaineistot)

The current target data in the backend is parsed from a `.dbf` file obtained from Museovirasto. The [tools folder](https://github.com/Sukeltaja-App/tools/blob/master/parse_mj_rekisteri/) has a parsed [targets.json](https://github.com/Sukeltaja-App/tools/blob/master/parse_mj_rekisteri/targets.json) file that is directly compatible with the backend.

## The Museovirasto WFS Server

[What's WFS?](https://en.wikipedia.org/wiki/Web_Feature_Service)

There were plans to add data from Museovirasto's WFS server instead of a static file. However, unlike the static file, supposedly the WFS server only contains data of shipwrecks that are over 100 years old.

Probably you would need to combine the existing [targets.json](https://github.com/Sukeltaja-App/tools/blob/master/parse_mj_rekisteri/targets.json) with the data from the WFS server.

The server address is: http://kartta.nba.fi/arcgis/services/WFS/MV_KulttuuriymparistoSuojellut/MapServer/WFSServer

## How to WFS

[There's a good general guide on accessing WFS servers here](https://docs.geoserver.org/latest/en/user/services/wfs/reference.html).

WFS servers can be accessed with normal [GET requests](https://en.wikipedia.org/wiki/GET_(HTTP)). The requests have a number of parameters that are important. The most important parameters are `version`, `service` and `request`.

The server gives back an XML file (that can have a size of several megabytes!). Usually you get back some general information about the request and the number of items returned followed by the list of the items.

There's a list of some basic requests below. It's advisable to use a modern REST client such as [Insomnia](https://insomnia.rest/) to access the server.

Happy XML parsing! 😊

### GetCapabilities

Get basic information about the capabilities of the server.

http://kartta.nba.fi/arcgis/services/WFS/MV_KulttuuriymparistoSuojellut/MapServer/WFSServer?version=2.0.0&request=GetCapabilities&service=wfs

### DescribeFeatureType

Return a description of feature types supported by the server.

http://kartta.nba.fi/arcgis/services/WFS/MV_KulttuuriymparistoSuojellut/MapServer/WFSServer?version=2.0.0&request=DescribeFeatureType&service=wfs

### List of underwater targets

It's a bit trickier to get useful data, such as a list of underwater targets. The filtering of data is done using the [OGC Filter Encoding standard](https://docs.geoserver.org/stable/en/user/filter/filter_reference.html#filter-fe-reference), which is basically just XML encoded with a custom namespace.

Use the following parameters:

- `version=2.0.0`
- `service=wfs`
- `request=GetFeature`
- `typeNames=Muinaisjaannokset_piste`
- `propertyName=mjtunnus,inspireID,kohdenimi,kunta,laji,tyyppi,alatyyppi,ajoitus,vedenalainen,muutospvm,luontipvm,paikannustapa,paikannustarkkuus,selite,url,x,y`
- `FILTER=`

```
<ogc:Filter>
  <Or>
    <PropertyIsEqualTo>
      <PropertyName>vedenalainen</PropertyName>
      <Literal>k</Literal>
    </PropertyIsEqualTo>
    <PropertyIsEqualTo>
      <PropertyName>vedenalainen</PropertyName>
      <Literal>K</Literal>
    </PropertyIsEqualTo>
  </Or>
</ogc:Filter>
```

to generate a request that looks like this:

http://kartta.nba.fi/arcgis/services/WFS/MV_KulttuuriymparistoSuojellut/MapServer/WFSServer?version=2.0.0&request=GetFeature&typeNames=Muinaisjaannokset_piste&service=wfs&propertyName=mjtunnus,inspireID,kohdenimi,kunta,laji,tyyppi,alatyyppi,ajoitus,vedenalainen,muutospvm,luontipvm,paikannustapa,paikannustarkkuus,selite,url,x,y&FILTER=%3Cogc%3AFilter%3E%0A%20%20%3COr%3E%0A%20%20%20%20%3CPropertyIsEqualTo%3E%0A%20%20%20%20%20%20%3CPropertyName%3Evedenalainen%3C%2FPropertyName%3E%0A%20%20%20%20%20%20%3CLiteral%3Ek%3C%2FLiteral%3E%0A%09%20%20%3C%2FPropertyIsEqualTo%3E%0A%20%20%20%20%3CPropertyIsEqualTo%3E%0A%20%20%20%20%20%20%3CPropertyName%3Evedenalainen%3C%2FPropertyName%3E%0A%20%20%20%20%20%20%3CLiteral%3EK%3C%2FLiteral%3E%0A%09%20%20%3C%2FPropertyIsEqualTo%3E%0A%20%20%3C%2FOr%3E%0A%3C%2Fogc%3AFilter%3E

### List of shipwrecks

Use the following parameters:

- `version=2.0.0`
- `service=wfs`
- `request=GetFeature`
- `typeNames=Muinaisjaannokset_piste`
- `propertyName=mjtunnus,inspireID,kohdenimi,kunta,laji,tyyppi,alatyyppi,ajoitus,vedenalainen,muutospvm,luontipvm,paikannustapa,paikannustarkkuus,selite,url,x,y`
- `FILTER=`
```
<ogc:Filter>
  <PropertyIsLike wildCard="*" singleChar="." escape="\">
    <PropertyName>tyyppi</PropertyName>
    <Literal>alusten hylyt*</Literal>
  </PropertyIsLike>
</ogc:Filter>
```

to generate a request that looks like this:

http://kartta.nba.fi/arcgis/services/WFS/MV_KulttuuriymparistoSuojellut/MapServer/WFSServer?version=2.0.0&request=GetFeature&typeNames=Muinaisjaannokset_piste&service=wfs&propertyName=mjtunnus,inspireID,kohdenimi,kunta,laji,tyyppi,alatyyppi,ajoitus,vedenalainen,muutospvm,luontipvm,paikannustapa,paikannustarkkuus,selite,url,x,y&FILTER=%3Cogc%3AFilter%3E%0A%20%20%3CPropertyIsLike%20wildCard%3D%22*%22%20singleChar%3D%22.%22%20escape%3D%22%5C%22%3E%0A%20%20%20%20%3CPropertyName%3Etyyppi%3C%2FPropertyName%3E%0A%20%20%20%20%3CLiteral%3Ealusten%20hylyt*%3C%2FLiteral%3E%0A%20%20%3C%2FPropertyIsLike%3E%0A%3C%2Fogc%3AFilter%3E

### List of all targets (Muinaisjaannokset_piste)

A list of all targets without any filtering. Includes only the id `mjtunnus` and type `tyyppi` of the target.

⚠️ Warning: this request can take minutes to complete as it returns an XML file of 37338 targets with a file size of 15.2 Mb.

http://kartta.nba.fi/arcgis/services/WFS/MV_KulttuuriymparistoSuojellut/MapServer/WFSServer?version=2.0.0&request=GetFeature&typeNames=Muinaisjaannokset_piste&service=wfs&propertyName=mjtunnus,tyyppi
