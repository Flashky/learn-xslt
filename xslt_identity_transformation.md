# XSLT - Copiar, modificar y borrar árboles XML en su totalidad

Una de las grandes potencias de XSLT es coger un gran árbol XML, copiarlo y modificar, añadir o borrar un solo dato manteniendo el resto de la estructura igual que estaba antes.

Los siguientes ejemplos ilustran como hacer algunas de estas transformaciones.

## Copiar todo un árbol

La copia de un árbol se hace de manera recursiva. Lo que se hace es crear una copia, de las plantillas que son hijo de la plantilla actual:

```xslt
<xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

  <!-- Copy whole XML tree -->
  <xsl:template match="@*|node()">
      <xsl:copy>
          <xsl:apply-templates select="@*|node()"/>
      </xsl:copy>
  </xsl:template>
  
</xsl:stylesheet>
```

## Borrar un elemento de un árbol

Para borrar un elemento del fichero xml basta con crear una plantilla referida a dicho elemento y no meter nada dentro de la misma:

```xslt
<!-- Delete certain node -->
<xsl:template match="parentNode/childNode" />
```

Si lo conjuntásemos con la copia completa anterior, se copiaría todo el árbol, menos todos aquellos nodo denominados childNode que cuelguen de un nodo llamado parentNode:

```xslt
<xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

  <!-- Copy whole XML tree -->
  <xsl:template match="@*|node()">
      <xsl:copy>
          <xsl:apply-templates select="@*|node()"/>
      </xsl:copy>
  </xsl:template>
  
  <!-- Delete certain node -->
  <xsl:template match="parentNode/childNode" />
  
</xsl:stylesheet>
```

## Modificar un elemento del árbol

Para modificar un elemento del fichero xml, creamos una plantilla que coincida con dicho elemento, y en su cuerpo, introducimos las modificaciones que queramos realizar:

```xslt
  <!-- Change childNode content to childNodeNew content -->
  <xsl:template match="parentNode/childNode">
    <childNodeNew>Hola mundo!</childNodeNew>
  </xsl:template>
```

En el anterior caso, buscamos los nodos childNode que cuelguen de parentNodes y los sustituimos por un nodo childNodeNew que contiene un Hola mundo! en su interior.

Si lo conjuntásemos con la copia completa anterior, se copiaría todo el árbol, menos todos aquellos nodo denominados childNode que cuelguen de un nodo llamado parentNod los cuales, los modificaría como hemos visto anteriormente:

```xslt
<xsl:stylesheet version="2.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">

  <!-- Copy whole XML tree -->
  <xsl:template match="@*|node()">
      <xsl:copy>
          <xsl:apply-templates select="@*|node()"/>
      </xsl:copy>
  </xsl:template>
  
  <!-- Change childNode content to childNodeNew content -->
  <xsl:template match="parentNode/childNode">
    <childNodeNew>Hola mundo!</childNodeNew>
  </xsl:template>
  
</xsl:stylesheet>
```
