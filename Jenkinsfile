pipeline {
    agent any
    environment {
        RUBY_HOME="/usr/local/opt/ruby/bin"
        GEM_PATH="/usr/local/opt/ruby/lib/ruby/gems/2.7.0"
        GEM_HOME="$GEM_PATH"
        PATH="$RUBY_HOME:$GEM_HOME/bin:$PATH"
        LC_ALL = 'en_US.UTF-8'
        LANG    = 'en_US.UTF-8'
        LANGUAGE = 'en_US.UTF-8'
    }
    stages {
        stage('Checkout') {
            steps {
                echo 'Checkout..'
                checkout scm
            }
        }

        
        stage('Build') {
            steps {
                nodejs('NodeJS-14.10') {

                    echo 'Setup…'

                    sh ("""
                        set -e
                        # Set up Ruby dependencies via Bundler.
                        gem install bundler --conservative
                        bundle check || bundle install
                        bundle update
                        echo "Install yarn"
                        # Set up JS dependencies via Yarn.
                        npm install -g yarn
                        echo "install modules"
                        yarn install --modules-folder ./_assets/yarn
                    """)
                        echo 'Build…'
                    sh  ("""
                        set -e

                        echo "Started deploying"
                        
                        # Checkout gh-pages branch.
                        if [ `git branch | grep gh-pages` ]
                        then
                          git branch -D gh-pages
                        fi
                        git checkout -b gh-pages
                        
                        # Build site.
                        yarn install --modules-folder ./_assets/yarn
                        bundle exec jekyll build
                        
                        # Delete and move files.
                        find . -maxdepth 1 ! -name '_site' ! -name '.git' ! -name '.gitignore' -exec rm -rf {} \\;
                        mv _site/* .
                        rm -R _site/

                        echo "Deployed Successfully!"
                        
                        exit 0
                    """)
                }
                echo 'Done'
            }
        }
        stage('Publish') {
            steps {
                withCredentials([sshUserPrivateKey(credentialsId: '70b1cba3-b5b8-4470-b05d-9811ae10db1a', keyFileVariable: '', passphraseVariable: '', usernameVariable: '')]) {

                sh ("""
                git add -fA
                git commit --allow-empty -m "\$(git log -1 --pretty=%B) [ci skip]"
                git push -f -q origin gh-pages
                """)
}
            }
        }
    }
}