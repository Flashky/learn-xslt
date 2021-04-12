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
