# Tarea-1-DADM-Modulo-6

 Investigar elementos y/o bibliotecas que ayuden al consumo de REST APIs en Android.

# Instrucciones

1. Investigue qué es una clase POJO en Java, su equivalente en Kotlin y alguna herramienta que le ayude a generarlos fácil y rápidamente.


2. Busque la librería Glide y Picasso en Android. Indique para qué nos sirven e incluya un ejemplo de uso de cada una en una app (agregando el código Kotlin y comentando su implementación).
3. Agregue sus referencias.

# 1. POJO Class

### POJO Sample Code

```java
package com.integrallis.TechConf.domain;
...
import org.apache.commons.lang.builder.EqualsBuilder;
import org.apache.commons.lang.builder.HashCodeBuilder;
import org.apache.commons.lang.builder.ToStringBuilder;

public class Address implements Serializable {
    // primary key
    private Integer id;
    // fields
    private String streetAddress;
    private String state;
    private String zipCode;
    private String city;
    private String aptNumber;

    // constructors
    public Address () {}

    // ...getters and setters
    /* Implementation of equals using Business Key Equality
     *
     * (non-Javadoc)
     * @see java.lang.Object#equals(java.lang.Object)
     */

    public boolean equals (Object object) {
        // short circuits
        if (object == null) return false;
        if (this == object) return true;
        if (!(object instanceof Address)) return false;
        final Address address = (Address) object;
        //NOTE always use getters on the passed object since it // might be a Hibernate Proxy
        return new EqualsBuilder().
            append(streetAddress, address.getStreetAddress()).
            append(aptNumber, address.getAptNumber()).
            append(city, address.getCity()).
            append(state, address.getState()).
            append(zipCode, address.getZipCode()).
            isEquals();
    }

    public int hashCode () {
        // pick a hard-coded, randomly chosen, non-zero, odd number
        // ideally different for each class
        return new HashCodeBuilder(17, 37).
            append(streetAddress).
            append(aptNumber).
            append(city).
            append(state).
            append(zipCode).
            toHashCode();
    }
    
    public String toString () {
        return new ToStringBuilder(this).
            append("streetAddress", streetAddress).
            append("aptNumber", aptNumber).
            append("city", city).
            append("state", state).
            append("zipCode", zipCode).
            toString();
    }
}
```

# 2. GLIDE and PICASSO Libraries in Android

# 3. Referencias
