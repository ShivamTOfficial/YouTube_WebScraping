# YouTube_WebScraping

First off, we import a package called **google-api-python-client**
1. On Command Line Type *pip install google-api-python-client*
2. On Anaconda Prompt Type *conda install -c conda-forge google-api-python-client*


& then an API Key needs to be created, which I did using [Google Developers Console](https://console.developers.google.com/).

    from googleapiclient.discovery import build
    
We copy the API Key from Google Developers Console and make a variable by the same name

    api_key = 'AIzaSyCTVT2ssuK5yiOOJ9KFaZq6JJpVuebdiyM'

### Fetching the Channel IDs of our favourite channels. 
( [Watch this video to see how to do that (will upload soon...)]() )

    channel_ids = ['UCHnyfMqiRRG1u-2MsSQLbXA', # Veritasium
                   'UCcZhBlipmIFlfZjt-Ji4Udg', # Conor Neill
                   'UCOajpsI8t3Eg-u-s2j_c-cQ', # Movie Flame
                   'UChYfrRp_CWyqOt-ZYJGOgmA', # Chuck Severance
                   'UC2UXDak6o7rBm23k3Vv5dww'  # Dhruv Rathee 
                  ]

    youtube = build('youtube', 'v3', developerKey=api_key)
    
    
### Function to get Channel Statistics

    def get_channel_stats(youtube, channel_ids):
    all_data = []
    request = youtube.channels().list(
                part='snippet,contentDetails,statistics',
                id=','.join(channel_ids))
    response = request.execute() 
    
    for i in range(len(response['items'])):
        data = dict(Channel_name = response['items'][i]['snippet']['title'],
                    Subscribers = response['items'][i]['statistics']['subscriberCount'],
                    Views = response['items'][i]['statistics']['viewCount'],
                    Total_videos = response['items'][i]['statistics']['videoCount'],
                    playlist_id = response['items'][i]['contentDetails']['relatedPlaylists']['uploads'])
        all_data.append(data)
    
    return all_data
    
### Get Channel Stats
    
    channel_statistics = get_channel_stats(youtube, channel_ids)
    channel_data = pd.DataFrame(channel_statistics)
    channel_data
    
### Creating CSV file of data
    channel_data.to_csv('blablablah.csv', index = False)
    
    
### Count Of Subscribers/ Views/ Total Videos
    channel_data['Subscribers'] = pd.to_numeric(channel_data['Subscribers'])
    channel_data['Views'] = pd.to_numeric(channel_data['Views'])
    channel_data['Total_videos'] = pd.to_numeric(channel_data['Total_videos'])
    channel_data.dtypes

### Visualizing the Results

    sns.set(rc={'figure.figsize':(10,8)})
    ax = sns.barplot(x='Channel_name', y='Subscribers', data=channel_data)
