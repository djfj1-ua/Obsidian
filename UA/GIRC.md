## Práctica 1
Primero he borrado la VPC que venia por defecto de AWS y he creado la mía propia my-vpc. La red es 192.168.0.0/24 de clase C.![[Pasted image 20250207183611.png]]
Ahora, creare las subredes. Son 2 privadas y una pública. Las subredes tendrán máscara de red de 26 bits para poder crear 4 subredes, de las cuales solo usaremos 3.
![[Pasted image 20250207184440.png]]
Tenemos que crear las 3 instancias EC2, hay que crear una en la subred privada 1, otra en la subred privada 2 y otra en la subred pública. En la instancia de la subred pública hay que habilitar que se genere la ip pública automáticamente.