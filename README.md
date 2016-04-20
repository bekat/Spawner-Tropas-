# Spawner-Tropas-
Spawner troops similar league of leyends

// PRACTICA SPAWNER LEAGUE OF LEYENDS PARA TRINIT
// Creado por : David Sanz Navarro
// El script consta de un spawner basico que cada 10 segundos
// salen 3 tropas cuerpo a cuerpo, 3 tropas a distancia,
// 1 tropa de asedio solo si las oleadas son impares.

// Hay programada una autodestruccion del inhibidor a los 30´´
// y entonces salen las 3 tropas cuerpo a cuerpo 
// 3 tropas a distancia y 1 de asedio MAS GRANDE

using UnityEngine;
using System.Collections;

public class PracticaSpawner : MonoBehaviour {

	public GameObject tropa1;
	public GameObject tropa2;
	public GameObject tropa3;
	public GameObject tropa4;
	public GameObject inhibidor;

	public int CantidadTropas = 3;
	public int contadorOleadas;

	private GameObject tropa1Clon;
	private GameObject tropa2Clon;
	private GameObject tropa3Clon;
	private GameObject tropa4Clon;

	public float contador = 0f;
	public float contadorMax = 10f;
	public float radio = 10f;


	void Update () {


		// Destruimos el inhibidor a los 20 segundos
		Destroy (inhibidor, 30f);

		// Posicionamos las instancias en un radio de X en la superficie
		Vector3 posicion = Random.insideUnitSphere * radio;
		posicion.y = 0f;


		// Contador necesario para la salida de nuevas oleadas
		contador = contador + 1f * Time.deltaTime;


		if (contador < contadorMax)
			return;

		// Si NO esta el inhibidor en pantalla salen estas tropas
		if (inhibidor == false) {

			tropa1Clon = Instantiate (tropa4,
				new Vector3 (Random.Range (-500f,500f), 0, Random.Range (-500f,500f)) + posicion, transform.rotation) as GameObject;
			

			for (int i = 0; i < CantidadTropas; i++) {
				
				tropa1Clon = Instantiate (tropa1,
					new Vector3 (Random.Range (-500f, 500f), 0, Random.Range (-500f, 500f)) + posicion, transform.rotation) as GameObject;


				tropa2Clon = Instantiate (tropa2,
					new Vector3 (Random.Range (-500f, 500f), 0, Random.Range (-500f, 500f)) + posicion, transform.rotation) as GameObject;

				}


		// SI esta el inhibidor en pantalla salen estas tropas
		} else {

			for (int i = 0; i < CantidadTropas; i++) {

				tropa1Clon = Instantiate (tropa1,
					new Vector3 (Random.Range (-500f,500f), 0, Random.Range (-500f,500f)) + posicion, transform.rotation) as GameObject;

				tropa2Clon = Instantiate (tropa2,
					new Vector3 (Random.Range (-500f,500f), 0, Random.Range (-500f,500f)) + posicion, transform.rotation) as GameObject;

			}

			// Este tipo de tropa sale exclusivamente con las oleadas impares
			if (contadorOleadas % 2 == 0) {

				tropa3Clon = Instantiate (tropa3,
					new Vector3 (Random.Range (-500f,500f), 0, Random.Range (-500f,500f)) + posicion, transform.rotation) as GameObject;

			}


		}

			contadorOleadas++;
			contador = 0f;

	}
}
