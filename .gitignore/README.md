# LISTA_ENLAZADA_SIMPLE
Reserva dinámica de memoria: malloc y free
/*LISTA ENLAZADA SIMPLE(COLECCIONES):Acceso aleatorio en memoria[ARRAY]
LISTA:Acceso no aleatorio*/

//elemento de la lista enlazada

typedef struct nodo {
	int dato;
	struct nodo* siguiente;//Puntero de enlace de tipo nodo que apunta hacia él mismo

}nodo_t;
nodo_t* head;//cabecera primer elemento
			 //operadores
nodo_t* nuevo_elemento() {
	nodo_t* elem = NULL;//apunto inicialmente al final de la lista
	elem = (nodo_t*)malloc(sizeof(nodo_t));
	if (elem == NULL) {
		puts("ERROR EN LA RESERVA DE MEMORIA¡¡");
	}
	return elem;
}
void init(int dato) {     //asignar espacio al primer elemento,reservar memoria
	head = nuevo_elemento();
	head->dato = dato;
	head->siguiente = NULL;
}
void insert_front(int dato) {//cambiar la cabeza por este elemento. Inserción al principio de la lista. Buscar el primer elemento, proporcionar memoria al nuevo elemento, generar el nuevo y ponerlo al principio.
	nodo_t* elem_nuevo;
	nodo_t* actual;
	//busco el primero
	actual = head;
	while (actual->siguiente != NULL)
		actual = actual->dato;
	//genero el nuevo
	elem_nuevo = (nodo_t*)malloc(sizeof(nodo_t));
	elem_nuevo->dato = dato;
	elem_nuevo->siguiente = NULL;
	//lo pongo al principio
	actual->dato = elem_nuevo;
}

void insert_back(int dato) {//Inserción al final de la lista
	nodo_t* elem_nuevo;
	nodo_t* actual;//añadir al final,buscar el ultimo elemento y luego genero el nuevo.Recorrer la lista con un bucle 
	//busco el ultimo
	actual = head;
	while (actual->siguiente != NULL) {
		actual = actual->siguiente;
	}
	//genero el nuevo
	elem_nuevo = (nodo_t*)malloc(sizeof(nodo_t));//proporcionar memoria al nuevo elemento
	elem_nuevo->dato = dato;
	elem_nuevo->siguiente = NULL;
	//lo pongo al final
	actual->siguiente = elem_nuevo;
}
void pop_back() {    //sacar y eliminar,quitar el ultimo elemento.Para poder quitar el ultimo que es NULL habria que buscar el penultimo.Utilizar free eliminando el ultimo elemento que es NULL, sabiendo cual es el penultimo elemento
	nodo_t* actual = NULL;
	nodo_t* anterior = NULL;
	actual = head;
	while (actual->siguiente != NULL) {
		anterior = actual;
		actual = actual->siguiente;
	}
	//borro el ultimo
	free(actual);
	anterior->siguiente = NULL;
}
void remove(int dato) {//eliminar la lista entera
	nodo_t* actual = NULL;
	nodo_t* anterior = NULL;
	if (!head) return -1;//no hay cabeza
	actual = head;
	//cabeza es el dato
	if (head->dato == dato) {
		head = actual->siguiente;
		free(actual);
		return dato;
	}
//cabeza no es el dato
	while (actual->siguiente != NULL) {
		anterior = actual;
		actual = actual->siguiente;

		//compruebo dato
		if (actual->dato == dato) {
			anterior->siguiente = actual->siguiente;
			free(actual);
			return dato;
		}
	}
	//no he borrado nada
	return -1;
}

void print() {//imprimir la lista
	nodo_t* actual = NULL;
	actual = head;
	while (actual != NULL) {
		actual = actual->siguiente;
		printf(actual);
	}
}
	int get_size() {//nunca se repite código
		int res = 0;
		nodo_t* actual = NULL;
		//if (!head) return 0;
		actual = head;
		while (actual!= NULL) {
			actual = actual->siguiente;
			res++;
		}
		return res;
	}
	int main(void) {
		//TEST UNITARIO
		init(10);
		insert_back(5);
		insert_back(8);
		print();
		remove(8);
		print();
		pop_back();
		printf("%d", get_size());
	}
