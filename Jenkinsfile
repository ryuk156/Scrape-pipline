 def repoLoad
 def repoScrape 
 def repoList


pipeline{
    agent any

    stages{
      stage('Gather module data'){
          steps{
               repoLoad= load 'Loadrepo.groovy'
              repoScrape = load 'Scrape.groovy'
              repoList = repoLoad.fetch()

              dir('meta-data'){
                  git url : "https://github.com/GooeyTests/TempIndex"
              }

            repoList.each {
			dir(it) {
				git url: "https://github.com/Terasology/${it}"
				repoScrape.exec()
			}


		   }
             
             dir('meta-data') {
			repoScrape.push()
		}

          }
      }
    }
}
