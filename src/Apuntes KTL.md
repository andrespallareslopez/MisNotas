# Proyecto KTL

netstat -aof | findstr :7000
netstat -aof | findstr :5672

Repositorio de Front de KTL KTL-Registrar

https://umane.everis.com/git/ADOCENALC/ktl-registrar

Repositorio de Back de KTL ktl-ECU

https://umane.everis.com/git/ADOCENALC/ktl-ecu

Repositorio de DeptApps pluggins nodos nuevos asociados a KTL

https://umane.everis.com/git/ADOCENALC/deptapps-flows-contrib-ktl

La aplicacion KTL en produccion su url:

https://ktl.alicante.deptapps.everis.cloud/

para ver en produccion algun proyecto de ktl en el boton claim meter lo siguiente:

nombre del proyecto:SDT

ID proyecto:4c43003c-9988-4b3a-a4f6-f0f8094550d9



Tenemos una serie de peticiones o url de back:

https://ktl.alicante.deptapps.everis.cloud/_next/data/mCb1CLmSHMZy1hw5PXahA/my-projects/SDT.json?projectKey=SDT

https://ktl.alicante.deptapps.everis.cloud/api/general/fields?projectKey=SDT

https://ktl.alicante.deptapps.everis.cloud/api/general/issuetypes?projectKey=SDT

https://ktl.alicante.deptapps.everis.cloud/_next/data/mCb1CLmSHMZy1hw5PXahA/my-projects/SDT/SANTALUCIATEST.json?projectKey=SDT&sourceId=SANTALUCIATEST


el detalle de cada peticion y que es lo que devuelve:


https://ktl.alicante.deptapps.everis.cloud/_next/data/mCb1CLmSHMZy1hw5PXahA/my-projects/SDT.json?projectKey=SDT

~~~
{
	"pageProps": {
		"project": {
			"id": "4c43003c-9988-4b3a-a4f6-f0f8094550d9",
			"projectKey": "SDT",
			"createdBy": "avizuete@emeal.nttdata.com",
			"createdOn": "2022-04-11T09:04:58.000Z",
			"sources": [
				{
					"id": "2",
					"projectKey": "SDT",
					"sourceName": "default",
					"defaultAssignee": "ahurtadg",
					"defaultIssueType": "10900",
					"createdBy": "SYSTEM",
					"createdOn": "2022-04-11T09:05:15.000Z",
					"keyFields": [
						"customfield_12049"
					],
					"rules": [
						{
							"id": "58",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "summary",
							"expression": "summary"
						},
						{
							"id": "59",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "description",
							"expression": "description"
						},
						{
							"id": "60",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "priority",
							"expression": "(USE_MAP 'Priority' Priority)"
						},
						{
							"id": "61",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_24800",
							"expression": "'Yes'"
						},
						{
							"id": "62",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "components",
							"expression": "'ATRIA-MOTOR'"
						},
						{
							"id": "63",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_12045",
							"expression": "'No'"
						},
						{
							"id": "64",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_12049",
							"expression": "Number"
						},
						{
							"id": "65",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_23208",
							"expression": "'Ready to Start'"
						},
						{
							"id": "66",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_24801",
							"expression": "'No'"
						},
						{
							"id": "67",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_24111",
							"expression": "[Parent Incident]"
						},
						{
							"id": "68",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_24112",
							"expression": "[External Ticket Number]"
						},
						{
							"id": "69",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_24116",
							"expression": "commentsAndWorkNotes"
						},
						{
							"id": "70",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_24117",
							"expression": "assignmentGroup"
						},
						{
							"id": "71",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_24118",
							"expression": "assignmentTo"
						},
						{
							"id": "72",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_24119",
							"expression": "tags"
						},
						{
							"id": "73",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_24120",
							"expression": "incidentState"
						},
						{
							"id": "74",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_24121",
							"expression": "(PARSE_DATE [Due date])"
						},
						{
							"id": "75",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_24122",
							"expression": "(PARSE_DATE [Opened])"
						},
						{
							"id": "76",
							"projectKey": "SDT",
							"sourceName": "default",
							"key": "customfield_24132",
							"expression": "incidentState"
						}
					],
					"maps": [
						{
							"id": "4",
							"projectKey": "SDT",
							"sourceName": "default",
							"name": "Priority",
							"entries": [
								{
									"id": "19",
									"mapId": "4",
									"key": "2 - Alta",
									"value": "High"
								},
								{
									"id": "20",
									"mapId": "4",
									"key": "3 - Medio",
									"value": "Medium"
								},
								{
									"id": "21",
									"mapId": "4",
									"key": "4 - Baja",
									"value": "Low"
								},
								{
									"id": "22",
									"mapId": "4",
									"key": "2 - High",
									"value": "High"
								},
								{
									"id": "23",
									"mapId": "4",
									"key": "3 - Medium",
									"value": "Medium"
								},
								{
									"id": "24",
									"mapId": "4",
									"key": "4 - Low",
									"value": "Low"
								}
							]
						}
					]
				},
				{
					"id": "6",
					"projectKey": "SDT",
					"sourceName": "CNSREFACT",
					"defaultAssignee": "eaguilar",
					"defaultIssueType": "10900",
					"createdBy": "SYSTEM",
					"createdOn": "2022-05-23T05:43:55.000Z",
					"keyFields": [
						"customfield_12049"
					],
					"rules": [
						{
							"id": "438",
							"projectKey": "SDT",
							"sourceName": "CNSREFACT",
							"key": "customfield_12049",
							"expression": "key"
						},
						{
							"id": "439",
							"projectKey": "SDT",
							"sourceName": "CNSREFACT",
							"key": "customfield_23601",
							"expression": "\"No\""
						},
						{
							"id": "440",
							"projectKey": "SDT",
							"sourceName": "CNSREFACT",
							"key": "customfield_24800",
							"expression": "\"Yes\""
						},
						{
							"id": "441",
							"projectKey": "SDT",
							"sourceName": "CNSREFACT",
							"key": "description",
							"expression": "description"
						},
						{
							"id": "442",
							"projectKey": "SDT",
							"sourceName": "CNSREFACT",
							"key": "issuetype",
							"expression": "\"Corrective\""
						},
						{
							"id": "443",
							"projectKey": "SDT",
							"sourceName": "CNSREFACT",
							"key": "priority",
							"expression": "\"Critical\""
						},
						{
							"id": "444",
							"projectKey": "SDT",
							"sourceName": "CNSREFACT",
							"key": "reporter",
							"expression": "\"eaguilar\""
						},
						{
							"id": "445",
							"projectKey": "SDT",
							"sourceName": "CNSREFACT",
							"key": "summary",
							"expression": "summary"
						},
						{
							"id": "446",
							"projectKey": "SDT",
							"sourceName": "CNSREFACT",
							"key": "labels",
							"expression": "labels"
						}
					],
					"maps": []
				},
				{
					"id": "7",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"defaultAssignee": "eaguilar",
					"defaultIssueType": "10900",
					"createdBy": "SYSTEM",
					"createdOn": "2022-05-23T06:51:36.000Z",
					"keyFields": [
						"customfield_12049"
					],
					"rules": [
						{
							"id": "310",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"key": "assignee",
							"expression": "u_providername"
						},
						{
							"id": "311",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"key": "components",
							"expression": "assignment_group"
						},
						{
							"id": "312",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"key": "customfield_12049",
							"expression": "number"
						},
						{
							"id": "313",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"key": "customfield_12063",
							"expression": "sys_created_on"
						},
						{
							"id": "314",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"key": "customfield_21900",
							"expression": "resolved_at"
						},
						{
							"id": "315",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"key": "customfield_24111",
							"expression": "rfc"
						},
						{
							"id": "316",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"key": "customfield_24112",
							"expression": "caller_id"
						},
						{
							"id": "317",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"key": "customfield_24132",
							"expression": "u_production"
						},
						{
							"id": "318",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"key": "customfield_24133",
							"expression": "category"
						},
						{
							"id": "319",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"key": "customfield_24800",
							"expression": "'Yes'"
						},
						{
							"id": "320",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"key": "description",
							"expression": "description"
						},
						{
							"id": "321",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"key": "labels",
							"expression": "cmdb_ci"
						},
						{
							"id": "322",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"key": "priority",
							"expression": "(USE_MAP 'Priority' priority)"
						},
						{
							"id": "323",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"key": "summary",
							"expression": "number ' - ' short_description"
						}
					],
					"maps": [
						{
							"id": "32",
							"projectKey": "SDT",
							"sourceName": "SANTALUCIATEST",
							"name": "Priority",
							"entries": [
								{
									"id": "121",
									"mapId": "32",
									"key": "1 - Crítica",
									"value": "Critical"
								},
								{
									"id": "122",
									"mapId": "32",
									"key": "2 - Alta",
									"value": "High"
								},
								{
									"id": "123",
									"mapId": "32",
									"key": "3 - Media",
									"value": "Medium"
								},
								{
									"id": "124",
									"mapId": "32",
									"key": "4 - Baja",
									"value": "Low"
								}
							]
						}
					]
				},
				{
					"id": "15",
					"projectKey": "SDT",
					"sourceName": "ENDESA",
					"defaultAssignee": "pperezro",
					"defaultIssueType": "10601",
					"createdBy": "SYSTEM",
					"createdOn": "2022-07-27T07:28:00.000Z",
					"keyFields": [
						"customfield_24111"
					],
					"rules": [
						{
							"id": "789",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "assignee",
							"expression": "'pperezro'"
						},
						{
							"id": "790",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "components",
							"expression": "'Test'"
						},
						{
							"id": "791",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "customfield_11628",
							"expression": "typeEvolutive"
						},
						{
							"id": "792",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "customfield_23208",
							"expression": "correctivePhase"
						},
						{
							"id": "793",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "customfield_23209",
							"expression": "evolutivePhase"
						},
						{
							"id": "794",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "customfield_23412",
							"expression": "'Blocked'"
						},
						{
							"id": "795",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "customfield_24111",
							"expression": "idTask"
						},
						{
							"id": "796",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "customfield_24800",
							"expression": "'Yes'"
						},
						{
							"id": "797",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "description",
							"expression": "description"
						},
						{
							"id": "798",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "issuetype",
							"expression": "issueType"
						},
						{
							"id": "799",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "labels",
							"expression": "tags"
						},
						{
							"id": "800",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "priority",
							"expression": "(USE_MAP 'Priority' priority)"
						},
						{
							"id": "801",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "reporter",
							"expression": "'pperezro'"
						},
						{
							"id": "802",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "summary",
							"expression": "summary"
						},
						{
							"id": "803",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"key": "customfield_23213",
							"expression": "(PARSE_DATE\n\ndateDelivery)"
						}
					],
					"maps": [
						{
							"id": "59",
							"projectKey": "SDT",
							"sourceName": "ENDESA",
							"name": "Priority",
							"entries": [
								{
									"id": "224",
									"mapId": "59",
									"key": "Baja",
									"value": "Low"
								},
								{
									"id": "225",
									"mapId": "59",
									"key": "Importante",
									"value": "High"
								},
								{
									"id": "226",
									"mapId": "59",
									"key": "Media",
									"value": "Medium"
								},
								{
									"id": "227",
									"mapId": "59",
									"key": "Urgente",
									"value": "Critical"
								}
							]
						}
					]
				},
				{
					"id": "16",
					"projectKey": "SDT",
					"sourceName": "ENDESA2",
					"defaultAssignee": "pperezro",
					"defaultIssueType": "10601",
					"createdBy": "SYSTEM",
					"createdOn": "2022-07-27T12:28:19.000Z",
					"keyFields": [
						"customfield_24111"
					],
					"rules": [
						{
							"id": "1062",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "assignee",
							"expression": "'pperezro'"
						},
						{
							"id": "1063",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "components",
							"expression": "Componente"
						},
						{
							"id": "1064",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "customfield_11628",
							"expression": "Tipo_Evolutivo"
						},
						{
							"id": "1065",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "customfield_23208",
							"expression": "(USE_MAP 'CorrectivePhase' Nombre_del_depósito)"
						},
						{
							"id": "1066",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "customfield_23209",
							"expression": "(USE_MAP 'EvolutivePhase' Nombre_del_depósito)"
						},
						{
							"id": "1067",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "customfield_23213",
							"expression": "(PARSE_DATE Fecha_de_vencimiento)"
						},
						{
							"id": "1068",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "customfield_23412",
							"expression": "(USE_MAP 'SupportPhase' Nombre_del_depósito)"
						},
						{
							"id": "1069",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "customfield_24111",
							"expression": "Id_de_tarea"
						},
						{
							"id": "1070",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "customfield_24800",
							"expression": "Facturable_Cliente"
						},
						{
							"id": "1071",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "description",
							"expression": "Descripción"
						},
						{
							"id": "1072",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "issuetype",
							"expression": "Tipo_Solicitud"
						},
						{
							"id": "1073",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "customfield_24112",
							"expression": "Etiquetas"
						},
						{
							"id": "1074",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "priority",
							"expression": "(USE_MAP 'Priority' Priority)"
						},
						{
							"id": "1075",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "reporter",
							"expression": "'pperezro'"
						},
						{
							"id": "1076",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"key": "summary",
							"expression": "Nombre_de_la_tarea"
						}
					],
					"maps": [
						{
							"id": "145",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"name": "CorrectivePhase",
							"entries": [
								{
									"id": "630",
									"mapId": "145",
									"key": "Pendiente",
									"value": "Under Study"
								},
								{
									"id": "631",
									"mapId": "145",
									"key": "En progreso",
									"value": "In Progress"
								},
								{
									"id": "632",
									"mapId": "145",
									"key": "Pendiente Validacion",
									"value": "Ready to Start"
								},
								{
									"id": "633",
									"mapId": "145",
									"key": "Finalizadas",
									"value": "Finished"
								},
								{
									"id": "634",
									"mapId": "145",
									"key": "Parado",
									"value": "Blocked"
								}
							]
						},
						{
							"id": "146",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"name": "EvolutivePhase",
							"entries": [
								{
									"id": "635",
									"mapId": "146",
									"key": "Pendiente",
									"value": "Under Study"
								},
								{
									"id": "636",
									"mapId": "146",
									"key": "En progreso",
									"value": "In Progress"
								},
								{
									"id": "637",
									"mapId": "146",
									"key": "Pendiente Validacion",
									"value": "Ready to Start"
								},
								{
									"id": "638",
									"mapId": "146",
									"key": "Finalizadas",
									"value": "Finished"
								},
								{
									"id": "639",
									"mapId": "146",
									"key": "Parado",
									"value": "Blocked"
								}
							]
						},
						{
							"id": "147",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"name": "Priority",
							"entries": [
								{
									"id": "640",
									"mapId": "147",
									"key": "Baja",
									"value": "Low"
								},
								{
									"id": "641",
									"mapId": "147",
									"key": "Importante",
									"value": "High"
								},
								{
									"id": "642",
									"mapId": "147",
									"key": "Media",
									"value": "Medium"
								},
								{
									"id": "643",
									"mapId": "147",
									"key": "Urgente",
									"value": "Critical"
								}
							]
						},
						{
							"id": "148",
							"projectKey": "SDT",
							"sourceName": "ENDESA2",
							"name": "SupportPhase",
							"entries": [
								{
									"id": "644",
									"mapId": "148",
									"key": "Pendiente",
									"value": "Under Study"
								},
								{
									"id": "645",
									"mapId": "148",
									"key": "En progreso",
									"value": "In Progress"
								},
								{
									"id": "646",
									"mapId": "148",
									"key": "Pendiente Validacion",
									"value": "Ready to Start"
								},
								{
									"id": "647",
									"mapId": "148",
									"key": "Finalizadas",
									"value": "Finished"
								},
								{
									"id": "648",
									"mapId": "148",
									"key": "Parado",
									"value": "Blocked"
								}
							]
						}
					]
				},
				{
					"id": "17",
					"projectKey": "SDT",
					"sourceName": "defaultfjfj",
					"defaultAssignee": "cgarmele",
					"defaultIssueType": "10601",
					"createdBy": "SYSTEM",
					"createdOn": "2022-08-26T11:47:51.000Z",
					"keyFields": [
						"summary"
					],
					"rules": [
						{
							"id": "1022",
							"projectKey": "SDT",
							"sourceName": "defaultfjfj",
							"key": "customfield_24802",
							"expression": "expression"
						}
					],
					"maps": []
				},
				{
					"id": "18",
					"projectKey": "SDT",
					"sourceName": "NATURGY",
					"defaultAssignee": "cgarmele",
					"defaultIssueType": "10601",
					"createdBy": "SYSTEM",
					"createdOn": "2022-08-26T11:55:00.000Z",
					"keyFields": [
						"customfield_24111"
					],
					"rules": [
						{
							"id": "1037",
							"projectKey": "SDT",
							"sourceName": "NATURGY",
							"key": "assignee",
							"expression": "\"cgarmele\""
						},
						{
							"id": "1038",
							"projectKey": "SDT",
							"sourceName": "NATURGY",
							"key": "components",
							"expression": "Componente"
						},
						{
							"id": "1039",
							"projectKey": "SDT",
							"sourceName": "NATURGY",
							"key": "customfield_23208",
							"expression": "Estado"
						},
						{
							"id": "1040",
							"projectKey": "SDT",
							"sourceName": "NATURGY",
							"key": "customfield_23209",
							"expression": "Estado"
						},
						{
							"id": "1041",
							"projectKey": "SDT",
							"sourceName": "NATURGY",
							"key": "customfield_23412",
							"expression": "Estado"
						},
						{
							"id": "1042",
							"projectKey": "SDT",
							"sourceName": "NATURGY",
							"key": "description",
							"expression": "Descripción"
						},
						{
							"id": "1043",
							"projectKey": "SDT",
							"sourceName": "NATURGY",
							"key": "issuetype",
							"expression": "Tipo_de_incidencia"
						},
						{
							"id": "1044",
							"projectKey": "SDT",
							"sourceName": "NATURGY",
							"key": "labels",
							"expression": "Etiquetas"
						},
						{
							"id": "1045",
							"projectKey": "SDT",
							"sourceName": "NATURGY",
							"key": "priority",
							"expression": "Prioridad"
						},
						{
							"id": "1046",
							"projectKey": "SDT",
							"sourceName": "NATURGY",
							"key": "summary",
							"expression": "Resumen"
						}
					],
					"maps": [
						{
							"id": "138",
							"projectKey": "SDT",
							"sourceName": "NATURGY",
							"name": "Corrective Phase Naturgy",
							"entries": [
								{
									"id": "596",
									"mapId": "138",
									"key": "Analisis - in progress",
									"value": "Under Study"
								},
								{
									"id": "597",
									"mapId": "138",
									"key": "En curso",
									"value": "In Construction"
								},
								{
									"id": "598",
									"mapId": "138",
									"key": "Pendiente de validar",
									"value": "Production pending"
								},
								{
									"id": "599",
									"mapId": "138",
									"key": "Finalizada",
									"value": "Delivered - Canceled"
								},
								{
									"id": "600",
									"mapId": "138",
									"key": "Blocked",
									"value": "Blocked"
								}
							]
						},
						{
							"id": "139",
							"projectKey": "SDT",
							"sourceName": "NATURGY",
							"name": "Evolutive Phase Naturgy",
							"entries": [
								{
									"id": "601",
									"mapId": "139",
									"key": "Analisis - in progress",
									"value": "Under Study"
								},
								{
									"id": "602",
									"mapId": "139",
									"key": "En curso",
									"value": "In Construction"
								},
								{
									"id": "603",
									"mapId": "139",
									"key": "Pendiente de validar",
									"value": "Production pending"
								},
								{
									"id": "604",
									"mapId": "139",
									"key": "Finalizada",
									"value": "Delivered - Canceled"
								},
								{
									"id": "605",
									"mapId": "139",
									"key": "Blocked",
									"value": "Blocked"
								}
							]
						},
						{
							"id": "140",
							"projectKey": "SDT",
							"sourceName": "NATURGY",
							"name": "Support Phase Naturgy",
							"entries": [
								{
									"id": "606",
									"mapId": "140",
									"key": "Analisis - in progress",
									"value": "Under Study"
								},
								{
									"id": "607",
									"mapId": "140",
									"key": "En curso",
									"value": "In Construction"
								},
								{
									"id": "608",
									"mapId": "140",
									"key": "Pendiente de validar",
									"value": "Production pending"
								},
								{
									"id": "609",
									"mapId": "140",
									"key": "Finalizada",
									"value": "Delivered - Canceled"
								},
								{
									"id": "610",
									"mapId": "140",
									"key": "Blocked",
									"value": "Blocked"
								}
							]
						}
					]
				},
				{
					"id": "19",
					"projectKey": "SDT",
					"sourceName": "Rally",
					"defaultAssignee": "onavarrl",
					"defaultIssueType": "10601",
					"createdBy": "SYSTEM",
					"createdOn": "2022-09-13T09:18:52.000Z",
					"keyFields": [
						"customfield_12049"
					],
					"rules": [
						{
							"id": "1212",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"key": "assignee",
							"expression": "assignee"
						},
						{
							"id": "1213",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"key": "components",
							"expression": "components"
						},
						{
							"id": "1214",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"key": "customfield_11628",
							"expression": "(USE_MAP 'TypeEvolutive' type_evolutive)"
						},
						{
							"id": "1215",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"key": "customfield_12032",
							"expression": "customfield_11400"
						},
						{
							"id": "1216",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"key": "customfield_12049",
							"expression": "key"
						},
						{
							"id": "1217",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"key": "customfield_22631",
							"expression": "customfield_14403"
						},
						{
							"id": "1218",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"key": "customfield_24121",
							"expression": "created"
						},
						{
							"id": "1219",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"key": "description",
							"expression": "description"
						},
						{
							"id": "1220",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"key": "issuetype",
							"expression": "(USE_MAP 'IssueType' issuetype)"
						},
						{
							"id": "1221",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"key": "labels",
							"expression": "labels"
						},
						{
							"id": "1222",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"key": "priority",
							"expression": "(USE_MAP 'Priority' Priority)"
						},
						{
							"id": "1223",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"key": "summary",
							"expression": "summary"
						}
					],
					"maps": [
						{
							"id": "173",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"name": "Comments",
							"entries": [
								{
									"id": "763",
									"mapId": "173",
									"key": "autor",
									"value": "user"
								},
								{
									"id": "764",
									"mapId": "173",
									"key": "comment",
									"value": "comment"
								}
							]
						},
						{
							"id": "174",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"name": "IssueType",
							"entries": [
								{
									"id": "765",
									"mapId": "174",
									"key": "Corrective",
									"value": "User Story"
								},
								{
									"id": "766",
									"mapId": "174",
									"key": "Sub-Construction",
									"value": "User Story"
								},
								{
									"id": "767",
									"mapId": "174",
									"key": "User Story",
									"value": "User Story"
								},
								{
									"id": "768",
									"mapId": "174",
									"key": "Technical task",
									"value": "User Story"
								},
								{
									"id": "769",
									"mapId": "174",
									"key": "Improvement",
									"value": "User Story"
								},
								{
									"id": "770",
									"mapId": "174",
									"key": "Bug",
									"value": "Sub-Defect"
								},
								{
									"id": "771",
									"mapId": "174",
									"key": "Sub-Technical task",
									"value": "Sub-Task"
								},
								{
									"id": "772",
									"mapId": "174",
									"key": "Epic",
									"value": "User Story"
								}
							]
						},
						{
							"id": "175",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"name": "Priority",
							"entries": [
								{
									"id": "773",
									"mapId": "175",
									"key": "Medium",
									"value": "Medium"
								},
								{
									"id": "774",
									"mapId": "175",
									"key": "Low",
									"value": "Low"
								},
								{
									"id": "775",
									"mapId": "175",
									"key": "Major",
									"value": "High"
								},
								{
									"id": "776",
									"mapId": "175",
									"key": "High",
									"value": "High"
								},
								{
									"id": "777",
									"mapId": "175",
									"key": "Trivial",
									"value": "Low"
								},
								{
									"id": "778",
									"mapId": "175",
									"key": "Critical",
									"value": "Critical"
								},
								{
									"id": "779",
									"mapId": "175",
									"key": "Blocker",
									"value": "Critical"
								},
								{
									"id": "780",
									"mapId": "175",
									"key": "Minor",
									"value": "Low"
								}
							]
						},
						{
							"id": "176",
							"projectKey": "SDT",
							"sourceName": "Rally",
							"name": "TypeEvolutive",
							"entries": [
								{
									"id": "781",
									"mapId": "176",
									"key": "Minor",
									"value": "Minor"
								}
							]
						}
					]
				}
			],
			"users": [
				{
					"username": "apallarl@emeal.nttdata.com"
				},
				{
					"username": "avizuete@emeal.nttdata.com"
				},
				{
					"username": "cgarmele@emeal.nttdata.com"
				},
				{
					"username": "egilprad@emeal.nttdata.com"
				},
				{
					"username": "fyankovi@emeal.nttdata.com"
				},
				{
					"username": "jbatistj@emeal.nttdata.com"
				},
				{
					"username": "lfernper@emeal.nttdata.com"
				},
				{
					"username": "onavarrl@emeal.nttdata.com"
				},
				{
					"username": "pjavaloy@emeal.nttdata.com"
				},
				{
					"username": "pperezro@emeal.nttdata.com"
				},
				{
					"username": "rob_eaguilar@everis.com"
				}
			],
			"employees": [
				{
					"employee": {
						"username": "avizuete"
					},
					"defaultEmployee": false
				},
				{
					"employee": {
						"username": "cgarmele"
					},
					"defaultEmployee": false
				},
				{
					"employee": {
						"username": "eaguilar"
					},
					"defaultEmployee": true
				},
				{
					"employee": {
						"username": "onavarrl"
					},
					"defaultEmployee": false
				},
				{
					"employee": {
						"username": "pperezro"
					},
					"defaultEmployee": false
				}
			]
		}
	},
	"__N_SSP": true
}

~~~


https://ktl.alicante.deptapps.everis.cloud/api/general/issuetypes?projectKey=SDT

~~~
[
	{
		"id": "10609",
		"name": "Sub-Functional Analysis",
		"subtask": true
	},
	{
		"id": "10613",
		"name": "Sub-Integrated Tests",
		"subtask": true
	},
	{
		"id": "13903",
		"name": "Sub-Global Management",
		"subtask": true
	},
	{
		"id": "15409",
		"name": "Sub-Unit Tests",
		"subtask": true
	},
	{
		"id": "10614",
		"name": "Sub-Management",
		"subtask": true
	},
	{
		"id": "15408",
		"name": "Sub-Requirements",
		"subtask": true
	},
	{
		"id": "10619",
		"name": "Sub-Support",
		"subtask": true
	},
	{
		"id": "15600",
		"name": "Doubt",
		"subtask": false
	},
	{
		"id": "15902",
		"name": "Management Incident",
		"subtask": false
	},
	{
		"id": "15901",
		"name": "Management Change",
		"subtask": false
	},
	{
		"id": "15406",
		"name": "Non Operative",
		"subtask": false
	},
	{
		"id": "15900",
		"name": "Risk",
		"subtask": false
	},
	{
		"id": "15405",
		"name": "Sub-Absence",
		"subtask": true
	},
	{
		"id": "15404",
		"name": "Sub-Presential",
		"subtask": true
	},
	{
		"id": "15410",
		"name": "Sub-Functional System Tests",
		"subtask": true
	},
	{
		"id": "14000",
		"name": "Evolutive",
		"subtask": false
	},
	{
		"id": "10601",
		"name": "Support",
		"subtask": false
	},
	{
		"id": "10900",
		"name": "Corrective",
		"subtask": false
	},
	{
		"id": "15419",
		"name": "Sub-Generic Subtask",
		"subtask": true
	},
	{
		"id": "10606",
		"name": "Sub-Construction",
		"subtask": true
	},
	{
		"id": "10608",
		"name": "Sub-Estimation",
		"subtask": true
	},
	{
		"id": "10607",
		"name": "Sub-Documentation",
		"subtask": true
	},
	{
		"id": "10000",
		"name": "Problem",
		"subtask": false
	},
	{
		"id": "15414",
		"name": "Sub-Peer Review",
		"subtask": true
	},
	{
		"id": "15413",
		"name": "Sub-Crossed Test",
		"subtask": true
	},
	{
		"id": "10200",
		"name": "Epic",
		"subtask": false
	},
	{
		"id": "15412",
		"name": "Sub-Acceptance Tests",
		"subtask": true
	},
	{
		"id": "15411",
		"name": "Sub-Non Functional System Tests",
		"subtask": true
	},
	{
		"id": "10620",
		"name": "Sub-Technical Design",
		"subtask": true
	},
	{
		"id": "15418",
		"name": "Sub-Doubt",
		"subtask": true
	},
	{
		"id": "15417",
		"name": "Sub-Defect",
		"subtask": true
	},
	{
		"id": "15416",
		"name": "Sub-Parametrization",
		"subtask": true
	},
	{
		"id": "15415",
		"name": "Sub-Deployment",
		"subtask": true
	}
]

~~~

https://ktl.alicante.deptapps.everis.cloud/api/general/fields?projectKey=SDT

~~~
[
	{
		"name": "Summary",
		"fieldId": "summary"
	},
	{
		"name": "Ready",
		"fieldId": "customfield_24802"
	},
	{
		"name": "Description",
		"fieldId": "description"
	},
	{
		"name": "Priority",
		"fieldId": "priority"
	},
	{
		"name": "Time Tracking",
		"fieldId": "timetracking"
	},
	{
		"name": "Change in scope",
		"fieldId": "customfield_24803"
	},
	{
		"name": "Subtask Expected start date",
		"fieldId": "customfield_23403"
	},
	{
		"name": "Subtask Expected end date",
		"fieldId": "customfield_23404"
	},
	{
		"name": "Sprint",
		"fieldId": "customfield_10700"
	},
	{
		"name": "Component/s",
		"fieldId": "components"
	},
	{
		"name": "Labels",
		"fieldId": "labels"
	},
	{
		"name": "Aggrupation",
		"fieldId": "customfield_12032"
	},
	{
		"name": "Service line",
		"fieldId": "customfield_12072"
	},
	{
		"name": "Visibility Group",
		"fieldId": "customfield_27200"
	},
	{
		"name": "Attachment",
		"fieldId": "attachment"
	},
	{
		"name": "Assignee",
		"fieldId": "assignee"
	},
	{
		"name": "Free Combo Field 1",
		"fieldId": "customfield_24132"
	},
	{
		"name": "Free Combo Field 2",
		"fieldId": "customfield_24133"
	},
	{
		"name": "Free Combo Field 3",
		"fieldId": "customfield_24134"
	},
	{
		"name": "Free Combo Field 4",
		"fieldId": "customfield_24135"
	},
	{
		"name": "Free Combo Field 5",
		"fieldId": "customfield_24136"
	},
	{
		"name": "Free Combo Field 6",
		"fieldId": "customfield_24137"
	},
	{
		"name": "Free Combo Field 7",
		"fieldId": "customfield_24138"
	},
	{
		"name": "Free Combo Field 8",
		"fieldId": "customfield_24139"
	},
	{
		"name": "Free Combo Field 9",
		"fieldId": "customfield_24140"
	},
	{
		"name": "Free Combo Field 10",
		"fieldId": "customfield_24141"
	},
	{
		"name": "Free Text Field 1",
		"fieldId": "customfield_24111"
	},
	{
		"name": "Free Text Field 2",
		"fieldId": "customfield_24112"
	},
	{
		"name": "Free Text Field 3",
		"fieldId": "customfield_24113"
	},
	{
		"name": "Free Text Field 4",
		"fieldId": "customfield_24114"
	},
	{
		"name": "Free Text Field 5",
		"fieldId": "customfield_24115"
	},
	{
		"name": "Free Text Field 6",
		"fieldId": "customfield_24116"
	},
	{
		"name": "Free Text Field 7",
		"fieldId": "customfield_24117"
	},
	{
		"name": "Free Text Field 8",
		"fieldId": "customfield_24118"
	},
	{
		"name": "Free Text Field 9",
		"fieldId": "customfield_24119"
	},
	{
		"name": "Free Text Field 10",
		"fieldId": "customfield_24120"
	},
	{
		"name": "Free Date Field 1",
		"fieldId": "customfield_24121"
	},
	{
		"name": "Free Date Field 2",
		"fieldId": "customfield_24122"
	},
	{
		"name": "Free Date Field 3",
		"fieldId": "customfield_24123"
	},
	{
		"name": "Free Date Field 4",
		"fieldId": "customfield_24124"
	},
	{
		"name": "Free Date Field 5",
		"fieldId": "customfield_24125"
	},
	{
		"name": "Free Date Field 6",
		"fieldId": "customfield_24127"
	},
	{
		"name": "Free Date Field 7",
		"fieldId": "customfield_24128"
	},
	{
		"name": "Free Date Field 8",
		"fieldId": "customfield_24129"
	},
	{
		"name": "Free Date Field 9",
		"fieldId": "customfield_24130"
	},
	{
		"name": "Free Date Field 10",
		"fieldId": "customfield_24131"
	},
	{
		"name": "Free Linked Combo Field 1",
		"fieldId": "customfield_26203"
	},
	{
		"name": "Free Linked Combo Field 2",
		"fieldId": "customfield_26204"
	},
	{
		"name": "Free Linked Combo Field 3",
		"fieldId": "customfield_26205"
	},
	{
		"name": "Free Linked Combo Field 4",
		"fieldId": "customfield_26206"
	},
	{
		"name": "Free Linked Combo Field 5",
		"fieldId": "customfield_26207"
	},
	{
		"name": "Form line",
		"fieldId": "customfield_11849"
	},
	{
		"name": "Free Linked Combo Field 6",
		"fieldId": "customfield_26208"
	},
	{
		"name": "Free Linked Combo Field 7",
		"fieldId": "customfield_26210"
	},
	{
		"name": "Free Linked Combo Field 8",
		"fieldId": "customfield_26211"
	},
	{
		"name": "Form line 2",
		"fieldId": "customfield_11850"
	},
	{
		"name": "Free Linked Combo Field 9",
		"fieldId": "customfield_26212"
	},
	{
		"name": "Free Linked Combo Field 10",
		"fieldId": "customfield_26213"
	},
	{
		"name": "Free Linked Combo Field 11",
		"fieldId": "customfield_26214"
	},
	{
		"name": "Form line 3",
		"fieldId": "customfield_11851"
	},
	{
		"name": "Free Linked Combo Field 12",
		"fieldId": "customfield_26215"
	},
	{
		"name": "Free Linked Combo Field 13",
		"fieldId": "customfield_26216"
	},
	{
		"name": "Form line 4",
		"fieldId": "customfield_11852"
	},
	{
		"name": "Free Linked Combo Field 14",
		"fieldId": "customfield_26217"
	},
	{
		"name": "Free Linked Combo Field 15",
		"fieldId": "customfield_26218"
	},
	{
		"name": "Project",
		"fieldId": "project"
	},
	{
		"name": "Issue Type",
		"fieldId": "issuetype"
	},
	{
		"name": "Parent",
		"fieldId": "parent"
	},
	{
		"name": "Reporter",
		"fieldId": "reporter"
	},
	{
		"name": "Billable to customer",
		"fieldId": "customfield_24800"
	},
	{
		"name": "Global Management Typology",
		"fieldId": "customfield_22630"
	},
	{
		"name": "Security Level",
		"fieldId": "security"
	},
	{
		"name": "Requirement Category 1",
		"fieldId": "customfield_11818"
	},
	{
		"name": "Requirement Category 2",
		"fieldId": "customfield_11819"
	},
	{
		"name": "Related issue",
		"fieldId": "customfield_23600"
	},
	{
		"name": "Date the incident occurs",
		"fieldId": "customfield_20458"
	},
	{
		"name": "Communicated by",
		"fieldId": "customfield_14300"
	},
	{
		"name": "Incident communication date",
		"fieldId": "customfield_20453"
	},
	{
		"name": "Responsible for receiving incident",
		"fieldId": "customfield_18300"
	},
	{
		"name": "Centers participate",
		"fieldId": "customfield_20464"
	},
	{
		"name": "Center",
		"fieldId": "customfield_20463"
	},
	{
		"name": "Responsible for managing incident",
		"fieldId": "customfield_20460"
	},
	{
		"name": "Personal data affected",
		"fieldId": "customfield_20454"
	},
	{
		"name": "Linked Issues",
		"fieldId": "customfield_20452"
	},
	{
		"name": "Opening date on client",
		"fieldId": "customfield_12063"
	},
	{
		"name": "Linked Issues",
		"fieldId": "issuelinks"
	},
	{
		"name": "Non Operative Type",
		"fieldId": "customfield_23000"
	},
	{
		"name": "Sale estimate (h)",
		"fieldId": "customfield_22631"
	},
	{
		"name": "Internal estimate (h)",
		"fieldId": "customfield_22634"
	},
	{
		"name": "Risk Managment Procedure",
		"fieldId": "customfield_11848"
	},
	{
		"name": "Type 2",
		"fieldId": "customfield_11854"
	},
	{
		"name": "Risk type",
		"fieldId": "customfield_11619"
	},
	{
		"name": "Category/ Subcategory",
		"fieldId": "customfield_11620"
	},
	{
		"name": "Text Selection Risk",
		"fieldId": "customfield_11853"
	},
	{
		"name": "Default Risk",
		"fieldId": "customfield_11621"
	},
	{
		"name": "Other Risk",
		"fieldId": "customfield_11610"
	},
	{
		"name": "As a result of",
		"fieldId": "customfield_10118"
	},
	{
		"name": "Can happen",
		"fieldId": "customfield_11845"
	},
	{
		"name": "Which would lead to",
		"fieldId": "customfield_11844"
	},
	{
		"name": "Action plan",
		"fieldId": "customfield_10128"
	},
	{
		"name": "Limit Date",
		"fieldId": "customfield_11609"
	},
	{
		"name": "Affected",
		"fieldId": "customfield_11622"
	},
	{
		"name": "Probability of the risk",
		"fieldId": "customfield_11623"
	},
	{
		"name": "Impact of the risk",
		"fieldId": "customfield_11624"
	},
	{
		"name": "Priority of the risk",
		"fieldId": "customfield_11625"
	},
	{
		"name": "Strategy",
		"fieldId": "customfield_11626"
	},
	{
		"name": "Resolved estimate",
		"fieldId": "customfield_24302"
	},
	{
		"name": "Contingency Solution",
		"fieldId": "customfield_11612"
	},
	{
		"name": "Contingency Trigger",
		"fieldId": "customfield_11613"
	},
	{
		"name": "ID client request",
		"fieldId": "customfield_12049"
	},
	{
		"name": "Abscence Typology",
		"fieldId": "customfield_22628"
	},
	{
		"name": "Presential Typology",
		"fieldId": "customfield_22629"
	},
	{
		"name": "Functional System Test Typology",
		"fieldId": "customfield_22632"
	},
	{
		"name": "Type Evolutive",
		"fieldId": "customfield_11628"
	},
	{
		"name": "Technology 1",
		"fieldId": "customfield_23210"
	},
	{
		"name": "Technology 2",
		"fieldId": "customfield_24000"
	},
	{
		"name": "Technology 3",
		"fieldId": "customfield_24001"
	},
	{
		"name": "Technology 4",
		"fieldId": "customfield_24002"
	},
	{
		"name": "Evolutive Phase",
		"fieldId": "customfield_23209"
	},
	{
		"name": "Excluded from ANS",
		"fieldId": "customfield_12045"
	},
	{
		"name": "Estimation Edit",
		"fieldId": "customfield_23212"
	},
	{
		"name": "Hitos",
		"fieldId": "customfield_18001"
	},
	{
		"name": "Expected start date",
		"fieldId": "customfield_23215"
	},
	{
		"name": "Expected delivery date",
		"fieldId": "customfield_23213"
	},
	{
		"name": "Versions Edit",
		"fieldId": "customfield_12074"
	},
	{
		"name": "Affects Version/s",
		"fieldId": "versions"
	},
	{
		"name": "Fix Version/s",
		"fieldId": "fixVersions"
	},
	{
		"name": "Other affected versions",
		"fieldId": "customfield_23214"
	},
	{
		"name": "Epic Link",
		"fieldId": "customfield_10701"
	},
	{
		"name": "Number of client requests",
		"fieldId": "customfield_12800"
	},
	{
		"name": "Theoretical estimate without Assets",
		"fieldId": "customfield_26912"
	},
	{
		"name": "Active automation",
		"fieldId": "customfield_26900"
	},
	{
		"name": "Active Functionality",
		"fieldId": "customfield_26904"
	},
	{
		"name": "Actual profit in Hours",
		"fieldId": "customfield_26908"
	},
	{
		"name": "Active automation 2",
		"fieldId": "customfield_26901"
	},
	{
		"name": "Active Functionality 2",
		"fieldId": "customfield_26905"
	},
	{
		"name": "Actual profit in Hours 2",
		"fieldId": "customfield_26909"
	},
	{
		"name": "Active automation 3",
		"fieldId": "customfield_26902"
	},
	{
		"name": "Active Functionality 3",
		"fieldId": "customfield_26906"
	},
	{
		"name": "Actual profit in Hours 3",
		"fieldId": "customfield_26910"
	},
	{
		"name": "Active automation 4",
		"fieldId": "customfield_26903"
	},
	{
		"name": "Active Functionality 4",
		"fieldId": "customfield_26907"
	},
	{
		"name": "Actual profit in Hours 4",
		"fieldId": "customfield_26911"
	},
	{
		"name": "Support Phase",
		"fieldId": "customfield_23412"
	},
	{
		"name": "Convertible into upgrade",
		"fieldId": "customfield_24801"
	},
	{
		"name": "Corrective Phase",
		"fieldId": "customfield_23208"
	},
	{
		"name": "Problem Description",
		"fieldId": "customfield_11860"
	},
	{
		"name": "Date identified",
		"fieldId": "customfield_24303"
	},
	{
		"name": "Originator",
		"fieldId": "customfield_11858"
	},
	{
		"name": "Peer Review Typology",
		"fieldId": "customfield_23409"
	},
	{
		"name": "Crossed Test Typology",
		"fieldId": "customfield_23408"
	},
	{
		"name": "Epic Name",
		"fieldId": "customfield_10703"
	},
	{
		"name": "Business Value",
		"fieldId": "customfield_12080"
	},
	{
		"name": "Non Functional System Test Typology",
		"fieldId": "customfield_22635"
	},
	{
		"name": "Customer Visibility",
		"fieldId": "customfield_23601"
	},
	{
		"name": "Answer",
		"fieldId": "customfield_23602"
	},
	{
		"name": "Responsible for the answer",
		"fieldId": "customfield_23603"
	},
	{
		"name": "Criticality",
		"fieldId": "customfield_11810"
	},
	{
		"name": "Date of transition to Blocker",
		"fieldId": "customfield_23604"
	},
	{
		"name": "Location phase",
		"fieldId": "customfield_23605"
	},
	{
		"name": "Phase that originated the doubt",
		"fieldId": "customfield_23606"
	},
	{
		"name": "Incomplete Entry Documentation",
		"fieldId": "customfield_23607"
	},
	{
		"name": "Impact",
		"fieldId": "customfield_10901"
	},
	{
		"name": "Located in",
		"fieldId": "customfield_23200"
	},
	{
		"name": "Defect type",
		"fieldId": "customfield_23201"
	},
	{
		"name": "Origin",
		"fieldId": "customfield_23202"
	},
	{
		"name": "Causing subtask",
		"fieldId": "customfield_23203"
	},
	{
		"name": "Resolution estimate (h)",
		"fieldId": "customfield_23207"
	},
	{
		"name": "Expected end date",
		"fieldId": "customfield_13607"
	},
	{
		"name": "Real delivery date",
		"fieldId": "customfield_21900"
	},
	{
		"name": "Solved in the project",
		"fieldId": "customfield_23205"
	}
]
~~~

https://ktl.alicante.deptapps.everis.cloud/_next/data/mCb1CLmSHMZy1hw5PXahA/my-projects/SDT/SANTALUCIATEST.json?projectKey=SDT&sourceId=SANTALUCIATEST

~~~
{
	"pageProps": {
		"mode": "edit",
		"source": {
			"id": "7",
			"projectKey": "SDT",
			"sourceName": "SANTALUCIATEST",
			"defaultAssignee": "eaguilar",
			"defaultIssueType": "10900",
			"createdBy": "SYSTEM",
			"createdOn": "2022-05-23T06:51:36.000Z",
			"keyFields": [
				"customfield_12049"
			],
			"rules": [
				{
					"id": "310",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"key": "assignee",
					"expression": "u_providername"
				},
				{
					"id": "311",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"key": "components",
					"expression": "assignment_group"
				},
				{
					"id": "312",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"key": "customfield_12049",
					"expression": "number"
				},
				{
					"id": "313",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"key": "customfield_12063",
					"expression": "sys_created_on"
				},
				{
					"id": "314",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"key": "customfield_21900",
					"expression": "resolved_at"
				},
				{
					"id": "315",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"key": "customfield_24111",
					"expression": "rfc"
				},
				{
					"id": "316",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"key": "customfield_24112",
					"expression": "caller_id"
				},
				{
					"id": "317",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"key": "customfield_24132",
					"expression": "u_production"
				},
				{
					"id": "318",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"key": "customfield_24133",
					"expression": "category"
				},
				{
					"id": "319",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"key": "customfield_24800",
					"expression": "'Yes'"
				},
				{
					"id": "320",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"key": "description",
					"expression": "description"
				},
				{
					"id": "321",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"key": "labels",
					"expression": "cmdb_ci"
				},
				{
					"id": "322",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"key": "priority",
					"expression": "(USE_MAP 'Priority' priority)"
				},
				{
					"id": "323",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"key": "summary",
					"expression": "number ' - ' short_description"
				}
			],
			"maps": [
				{
					"id": "32",
					"projectKey": "SDT",
					"sourceName": "SANTALUCIATEST",
					"name": "Priority",
					"entries": [
						{
							"id": "121",
							"mapId": "32",
							"key": "1 - Crítica",
							"value": "Critical"
						},
						{
							"id": "122",
							"mapId": "32",
							"key": "2 - Alta",
							"value": "High"
						},
						{
							"id": "123",
							"mapId": "32",
							"key": "3 - Media",
							"value": "Medium"
						},
						{
							"id": "124",
							"mapId": "32",
							"key": "4 - Baja",
							"value": "Low"
						}
					]
				}
			]
		},
		"projectKey": "SDT"
	},
	"__N_SSP": true
}

~~~

Levantar API Rest nueva para KTL desde docker



## Instalar RabbitMQ con Docker ##


~~~
docker run -d --name rabbit -p 15672:15672 -p 5672:5672 rabbitmq:3-management
~~~


## Instalar Rabbitmq sin Doker para windows, instalacion local en nuestra maquina: ##


	
How To Install And Setup RabbitMQ Server Locally

https://www.c-sharpcorner.com/article/how-to-install-and-setup-rabbitmq-server-locally/



instalar los pluggin de rabbitmq
~~~
	
 cd C:\Program Files\RabbitMQ Server\rabbitmq_server-3.9.15\sbin

rabbitmq-plugins.bat enable rabbitmq_management

~~~







