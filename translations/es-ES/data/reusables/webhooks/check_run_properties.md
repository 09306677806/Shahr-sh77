| Clave                                   | Tipo        | Descripción                                                                                                                                                                                                                                                        |
| --------------------------------------- | ----------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| `Acción`                                | `secuencia` | La acción realizada. Puede ser una de las siguientes: <ul><li> `created` - Se creó una ejecución de verificación.</li><li> `completed` - El `status` de la ejecución de verificación es `completed`.</li><li> `rerequested` - Alguien volvió a solicitar que se volviera a ejecutar tu ejecución de verificación desde la IU de la solicitud de extracción. Consulta la sección "[Acerca de las verificaciones de estado](/articles/about-status-checks#checks)" para obtener más detalles sobre la IU de GitHub. Cuando recibes una acción de tipo `rerequested`, necesitarás [crear una ejecución de verificación nueva](/rest/reference/checks#create-a-check-run). Solo la {% data variables.product.prodname_github_app %} para la cual alguien solicitó volver a ejecutar la verificación recibirá la carga útil de `rerequested`.</li><li> `requested_action` - Alguien volvió a solicitar que se tome una acción que proporciona tu app. Solo la {% data variables.product.prodname_github_app %} para la cual alguien solicitó llevar a cabo una acción recibirá la carga útil de `requested_action`. Para aprender más sobre las ejecuciones de verificación y las acciones solicitadas, consulta la sección "[Ejecuciones de ferificación y acciones solicitadas](/rest/reference/checks#check-runs-and-requested-actions)."</li></ul>                                                                                                                                                                                     |
| `check_run`                             | `objeto`    | La [check_run](/rest/reference/checks#get-a-check-run).                                                                                                                                                                                                            |
| `check_run[status]`                     | `secuencia` | El estado actual de la ejecución de verificación. Puede ser `queued`, `in_progress`, o `completed`.                                                                                                                                                                |
| `check_run[conclusion]`                 | `secuencia` | El resultado de la ejecución de verificación que se completó. Puede ser uno de entre `success`, `failure`, `neutral`, `cancelled`, `timed_out`,  `action_required` o `stale`. Este valor será `null` hasta que la ejecución de verificación esté como `completed`. |
| `check_run[name]`                       | `secuencia` | El nombre de la ejecución de verificación.                                                                                                                                                                                                                         |
| `check_run[check_suite][id]`            | `número`    | La id de la suite de verificaciones de la cual es parte esta ejecución de verificación.                                                                                                                                                                            |
| `check_run[check_suite][pull_requests]` | `arreglo`   | Una matriz de solicitudes de extracción que empatan con esta suite de verificaciones. Una solicitud de cambios empata con una suite de verificaciones si tienen la misma `head_branch`.<br/><br/>**Nota:**<ul><li>El `head_sha` de la suite de verificaciones puede diferir del `sha` de la solicitud de cambios si se sube información subsecuentemente a la solicitud de cambios.</li><li>Cuando la `head_branch` de la suite de verificación está en un repositorio bifurcado, esta será `null` y el arreglo de `pull_requests` estará vacío.</li></ul>                    |
| `check_run[check_suite][deployment]`    | `objeto`    | Un despliegue a un ambiente de repositorio. Este solo se poblará si un job de flujo de trabajo de {% data variables.product.prodname_actions %} que referencia un ambiente crea la ejecución de verificación.                                                      |
| `requested_action`                      | `objeto`    | La acción que solicitó el usuario.                                                                                                                                                                                                                                 |
| `requested_action[identifier]`          | `secuencia` | La referencia del integrador de la acción que solicitó el usuario.                                                                                                                                                                                                 |