// groovy language
void theProcess(folder,image){
  def app
  script {
    stage("permissions") {
      dir(folder){
        sh "chmod 711 ./mvnw"
      }
    }
    stage("install"){
      dir(folder){
        sh "./mvnw -T 1C install -DskipTests"
      }
    }
    stage("build"){
      dir(folder){
        app = docker.build("ammonking/"+image)
      }
    }
    stage("deploy"){
      dir(folder){
        docker.withRegistry("https://registry.hub.docker.com","docker-hub-credentials") {
          app.push("${env.BUILD_NUMBER}")
          app.push("latest")
        }
      }
    }
  }

	pipeline{
		agent any 
			stages{
				state("automation"){
					parallel{
						stage("AdminServer"){
							steps{
								theProcess("AdminServer", "admin-server")
							}
						}
						stage("DiscoveryServer"){
							steps{
								theProcess("DiscoverServer", "discover-server")
							}
						}
						stage("PokemonService"){
							steps{
								theProcess("PokemonService", "pokemon-service")
							}
						}stage("TrainerService"){
							steps{
								theProcess("TrainerService", "trainer-service")
							}
						}
					}
				}
			}
	}










// node {

// 	/*copy of this in slack at 11:32 time 6/20/2019******* */

	
	
// 	def app

// 	stage("Clone repository"){
// 		/*clone the repository*/

// 		checkout scm
// 	}
// 	stage("Premissions"){
// 			parallel{
// 					stage("as permissions"){
// 						dir("AdminServer"){

// 						sh "chmod 711 ./mvnw"
// 					}
// 			}
// 				stage("as permissions"){
// 					dir("DiscoveryServer"){
// 						sh "chmod 711 ./mvnw"
// 				}
// 			}
// 		}
// 	}
	
	

// 	stage("Test"){
// 		dir("AdminServer"){

// 		/* run tests if they are there*/
// 		sh "./mvnw test"
// 	}
// 	}
// 	stage("Build Project"){
// 		dir("AdminServer"){
// 		/*get the project and build*/
// 		sh"./mvnw clean install"
// 		}
// 	}
// 		stage("Build Image"){
// 			app = docker.build("micknapp79/admin-server")
// 		}
// 		stage("Push Image"){
// 			dir("AdminServer"){
// 			/* push the image to docker hub */
// 		   		docker.withRegistry("https://registry.hub.doker.com","docker-hub-credentials"){
// 						 app.push("${env.BUILD_NUMBER}")
// 						 app.push("latest")
// 					 /*add more stages  and just use a pic of the jenkins pipeline showing they are trying to run and have a green chekmark*/

// 					}
// 				}
// 	}
// }