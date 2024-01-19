pipeline {
    agent any

    stages {
        stage('Deployment') {
            steps {
                script {
                    echo "--------------------------------"
                    echo "    Deployment Script Start     "
                    echo "--------------------------------"

                    // Function to prompt for user input and read the response
                    def prompt_for_input(question) {
                        return input(message: question, parameters: [string(defaultValue: '')])
                    }

                    // Function to confirm user's choice
                    def confirm_choice(question) {
                        def userInput = input(message: "${question} (yes/no)", parameters: [choice(choices: ['yes', 'no'], description: 'Choose', name: 'CHOICE')])
                        return userInput == 'yes'
                    }

                    // Default base folder
                    def default_base_folder = "/var/www"

                    // Prompt for Git username and PAT once
                    def git_user = prompt_for_input("Enter your Git username")
                    def pat = prompt_for_input("Enter your Personal Access Token (PAT)")

                    // Main deployment loop
                    while (true) {
                        // Prompt user for base folder with default option
                        def base_folder = prompt_for_input("Enter the path of the base folder (default: ${default_base_folder})")

                        if (base_folder == "") {
                            base_folder = default_base_folder
                        }

                        if (!confirm_choice("You have chosen the base folder as '${base_folder}'. Do you want to proceed?")) {
                            echo "Script aborted by user."
                            error "Script aborted by user."
                        }

                        // ... (rest of the script)

                        // Ask if the user wants to start another deployment
                        def continue_choice = prompt_for_input("Would you like to start another deployment? (yes/no)")
                        if (continue_choice.toLowerCase() != 'yes') {
                            echo "Exiting deployment script."
                            break
                        }
                    }
                }
            }
        }
    }
}
