# YouTube_WebScraping

First off, we import a package called **google-api-python-client**
1. On Command Line Type *pip install google-api-python-client*
2. On Anaconda Prompt Type *conda install -c conda-forge google-api-python-client*


& then an API Key needs to be created, which I did using [Google Developers Console](https://console.developers.google.com/).

    from googleapiclient.discovery import build
    
We copy the API Key from Google Developers Console and make a variable by the same name

    api_key = 'AIzaSyCTVT2ssuK5yiOOJ9KFaZq6JJpVuebdiyM'

Next, we need to get the Channel IDs of our favourite channels. [Watch this video for to see how to do that]()

    channel_ids = ['UCHnyfMqiRRG1u-2MsSQLbXA', # Veritasium
                   'UCLLw7jmFsvfIVaUFsLs8mlQ', # Luke Barousse 
                   'UCiT9RITQ9PW6BhXK0y2jaeg', # Ken Jee
                   'UC7cs8q-gJRlGwj4A8OmCmXg', # Alex the analyst
                   'UC2UXDak6o7rBm23k3Vv5dww' # Tina Huang
                  ]
