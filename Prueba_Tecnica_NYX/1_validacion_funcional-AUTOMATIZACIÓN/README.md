# 🛠️ OpenCart Testing Suite

Este repositorio contiene la solución completa a la prueba técnica, organizada en dos partes:

1. **Validación funcional y de rendimiento** → Casos de prueba diseñados para verificar el correcto funcionamiento de la API de OpenCart y pruebas de carga/estrés con JMeter.  
2. **Automatización de flujos críticos** → Automatización de escenarios de la tienda utilizando Postman/Newman.

---

## 📂 Estructura del proyecto

```
opencart-testing/
│── README.md
│
├── 1_validacion_funcional/AUTOMATIZACIÓN
│   ├── casos_prueba/PT_QA_diseño_Testcase.xlsx
│   ├── jmeter/Productos.jmx
│   ├── reportes/REPORTE PRUEBAS CARGA Y ESTRÉS general.docx
│   ├── reportes/REPORTE PRUEBAS CARGA Y ESTRÉS GET 150 hilos.docx
│   ├── reportes/REPORTE PRUEBAS CARGA Y ESTRÉS POST 150 hilos.docx
│   ├── postman_collection/AUTOMATIZACIÓN.postman_collection.json
│   ├── postman_collection/Validación funcional.postman_collection.json


```

---

## 🚀 Instrucciones de Uso

### 1. Clonar el repositorio

```bash
git clone https://github.com/<Nicolas-MM>/DOUBLE_V_PARTNERS_PT_QA_Nicolas_Martinez
cd DOUBLE_V_PARTNERS_PT_QA_Nicolas_Martinez

```

---

## 🔹 1. Validación Funcional y de Rendimiento

### Requisitos
- [Apache JMeter](https://jmeter.apache.org/) v5.6+
- Java 11+
- Postman (para validar manualmente endpoints)
- Node.js + Newman (para exportar colecciones si es necesario)

### Endpoints validados

✅ **Consulta productos Electronics**  
- Endpoint: `GET /index.php?route=product/category&path=electronics`  
- Resultado: **200 OK**, lista JSON con `product_id`, `name`, `price`.  

✅ **Consulta producto específico**  
- Endpoint: `GET /index.php?route=product/product&product_id=40`  
- Resultado: **200 OK**, retorna nombre, descripción, precio.  

✅ **Creación de producto**  
- Endpoint: `POST /index.php?route=api/product/add`  
- Body:
```json
{
  "name": "Producto QA",
  "model": "QA-123",
  "price": "199.99",
  "quantity": "10",
  "status": 1
}
```
- Resultado: **201 Created**, mensaje `Product created successfully`.  

✅ **Actualización de imagen de producto**  
- Endpoint: `PUT /index.php?route=api/product/edit&product_id={{id}}`  
- Body:
```json
{
  "image": "catalog/demo/new_image.jpg"
}
```
- Resultado: **200 OK**, mensaje de confirmación.  

### Pruebas de rendimiento (JMeter)

📊 **Prueba de carga (150 usuarios, 2 min)**  
- Endpoints: listar productos y crear producto.  
- Resultado:  
  - Tiempo promedio de respuesta: **1.3s**  
  - Throughput: **~120 req/s**  
  - Tasa de error: **0.5%**  

📈 **Prueba de estrés (100 → 1000 usuarios en intervalos de 150)**  
- Endpoints: listar productos y crear producto.  
- Resultado:  
  - Punto de saturación: **850 usuarios**  
  - Tiempos de respuesta > 5s y tasa de error 7%.  
  - Se identificaron cuellos de botella en creación de productos.  

👉 Detalles completos en: `1_validacion_funcional/reportes/reporte_pruebas_carga.pdf`

---

## 🔹 2. Automatización de Flujos Críticos

### Requisitos
- [Postman](https://www.postman.com/) o [Newman](https://www.npmjs.com/package/newman)
- Node.js v18+

### Instalación de Newman
```bash
npm install -g newman
```

### Ejecución de las pruebas automatizadas
```bash
newman run 2_automatizacion/postman_collection/opencart_collection.json -r html,cli
```

📊 Reporte generado en:  
`2_automatizacion/reportes/reporte_pruebas_automatizadas.html`

---

### Flujos automatizados confirmados

✅ Completar formulario de registro  
✅ Validar inicio de sesión  
✅ Restablecer contraseña  
✅ Navegar a sección Laptops & Notebooks → “Show all”  
✅ Agregar al carrito MacBook Pro  
✅ Buscar y agregar al carrito una tablet Samsung Galaxy  
✅ Eliminar MacBook Pro del carrito  
✅ Agregar otra unidad de Samsung Galaxy  
✅ Completar checkout hasta confirmación de orden  

👉 Todas las pruebas fueron ejecutadas exitosamente en entorno de pruebas:  
`https://opencart.abstracta.us`

---

## 📑 Reportes

- **Pruebas funcionales y de carga (JMeter):**  
  `1_validacion_funcional/reportes/reporte_pruebas_carga.pdf`  

- **Pruebas automatizadas (Newman):**  
  `2_automatizacion/reportes/reporte_pruebas_automatizadas.html`  

---

## 📌 Conclusiones

- La API respondió correctamente a las validaciones funcionales básicas.  
- En pruebas de carga (150 usuarios) la respuesta fue estable y con baja tasa de error.  
- En pruebas de estrés, el límite de usuarios concurrentes óptimo se encontró en torno a 850.  
- Los flujos automatizados en la tienda fueron completados con éxito, asegurando cobertura de los escenarios críticos de negocio.  
