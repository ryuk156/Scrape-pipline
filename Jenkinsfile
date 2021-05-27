pipeline{
    agent any

    stages{
      stage('Gather module data'){
          steps{
              def repoLoad= load 'Loadrepo.groovy'
              def repoScrape = load 'Scrape.groovy'
              def repoList = repoLoad.fetch()

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