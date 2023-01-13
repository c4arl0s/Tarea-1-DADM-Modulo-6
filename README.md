# Tarea-1-DADM-Modulo-6

- Nombre: Carlos Santiago Cruz
- Fecha: 13 de Enero del 2023

Investigar elementos y/o bibliotecas que ayuden al consumo de REST APIs en Android.

# Instrucciones

1. [Investigue qué es una clase POJO en Java, su equivalente en Kotlin y alguna herramienta que le ayude a generarlos fácil y rápidamente.](https://github.com/c4arl0s/Tarea-1-DADM-Modulo-6#1-pojo-class)
2. [Busque la librería Glide y Picasso en Android. Indique para qué nos sirven e incluya un ejemplo de uso de cada una en una app (agregando el código Kotlin y comentando su implementación).](https://github.com/c4arl0s/Tarea-1-DADM-Modulo-6#2-glide-and-picasso-libraries-in-android)
3. [Agregue sus referencias.](https://github.com/c4arl0s/Tarea-1-DADM-Modulo-6#3-referencias)

# [1. POJO Class](https://github.com/c4arl0s/Tarea-1-DADM-Modulo-6#tarea-1-dadm-modulo-6)

Java 2EE servia servia para desarrollar aplicaciones Enterprise con servicios transversales, de este se desprendian tres componentes principales:

1. Session Bean
2. Message Bean
3. Entity Bean (Complejo)

Cada una tenia una tarea muy en particular. Entity Bean manejaba objetos muy complejos, los cuales los persistia contra una base de datos. Estos contenian muchas interfaces.

Para solventar el problema nacio un framework llamado Hibernate, el cual usaba solo clases basicas o normales, y las cuales por su simplesa se podian persistir en la base de datos. A esta clase basica se le llamo POJO por sus siglas (Plain Old Java Object). 

### POJO Sample Code (Java Beans, special type of POJO classes)

```java
package com.integrallis.TechConf.domain;
...
import org.apache.commons.lang.builder.EqualsBuilder;
import org.apache.commons.lang.builder.HashCodeBuilder;
import org.apache.commons.lang.builder.ToStringBuilder;

public class Address implements Serializable { // must implement the Serializable interface

    // primary key
    private Integer id;

    // fields
    private String streetAddress;
    private String state;
    private String zipCode;
    private String city;
    private String aptNumber;

    // default no-argument constructor
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

# 2. [GLIDE and PICASSO Libraries in Android](https://github.com/c4arl0s/Tarea-1-DADM-Modulo-6#tarea-1-dadm-modulo-6)

# Glide

Glide es un rapido y eficiente framework para cargar y manejar imagenes. Es simple la manera en la que maneja la memoria y cache de disco para Android.
Glide soporta carga, decodificacion, imagenes,  GIFs animados y video. [Click para ir al repositorio](https://github.com/bumptech/glide)

Para su uso dentro de `onViewCreated()`, dentro de un fragment.

```kotlin
override fun onViewCreated(view: View, savedInstanceState: Bundle?) {
    super.onViewCreated(view, savedInstanceState)

    binding = FragmentDetailBinding.bind(view)
    user = args.user
    binding.user = args.user

    Glide.with(binding.root.context).load(user?.image).into(binding.userImageIV)
}
```

Para su uso dentro de una clase `ViewHolder` de un `RecyclerView`:

```kotlin
class UserViewHolder(private val binding: UserItemBinding) : RecyclerView.ViewHolder(binding.root) {

        fun bind(user: User, onItemClick: ((User) -> Unit)?) {

            binding.user = user
            Glide.with(binding.root).load(user.image).into(binding.userImageIV)

            binding.userCard.setOnClickListener {
                onItemClick?.invoke(user)
            }
        }
    }
```

![Screen Recording 2022-11-22 at 12 44 10 a m 2022-11-22 12_52_06 a m](https://user-images.githubusercontent.com/24994818/212422038-99835305-ebf5-4fd8-a351-d23889fffe22.gif)

# Picasso

Una potente biblioteca de descarga y almacenamiento en caché de imágenes para Android.
 
```java
Picasso.get().load("https://i.imgur.com/DvpvklR.png").into(imageView);
```

### AAdapter Downloads

La reutilización del adaptador se detecta automáticamente y la descarga anterior se cancela.

```java
@Override public void getView(int position, View convertView, ViewGroup parent) {
  SquaredImageView view = (SquaredImageView) convertView;
  if (view == null) {
    view = new SquaredImageView(context);
  }
  String url = getItem(position);

  Picasso.get().load(url).into(view);
}
```

### Transformacion de imagenes

```java
Picasso.get()
  .load(url)
  .resize(50, 50)
  .centerCrop()
  .into(imageView)
```

# 3. [Referencias](https://github.com/c4arl0s/Tarea-1-DADM-Modulo-6#tarea-1-dadm-modulo-6)

- Sam-Bodden, Brian (2006) Beginning POJOs: From Novice to Professional, New York, NY, Por Apress

