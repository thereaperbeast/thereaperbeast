import requests
import json

# replace 'your-api-key-here' with your Canvas API key
api_key = 'your-api-key-here'

# replace 'your-course-id-here' with the ID of your Canvas course
course_id = 'your-course-id-here'

# set up the API endpoint for upcoming assignments
url_thisweek = f'https://{your_canvas_domain}/api/v1/courses/{course_id}/assignments?per_page=100&sort=due_date'

# set up the headers for the API request
headers = {
    'Authorization': f'Bearer {api_key}',
}

# make the API request for upcoming assignments
response_thisweek = requests.get(url_thisweek, headers=headers)

# print the upcoming assignments
if response_thisweek.status_code == 200:
    assignments = json.loads(response_thisweek.text)
    for assignment in assignments:
        if assignment['due_at']:
            print(f'Assignment: {assignment["name"]}, Due: {assignment["due_at"]}')
else:
    print('Error: Failed to retrieve upcoming assignments.')

# set up the API endpoint for discussions topics
url_discussions = f'https://{your_canvas_domain}/api/v1/courses/{course_id}/discussion_topics'

# make the API request for discussions topics
response_discussions = requests.get(url_discussions, headers=headers)

# print the discussions topics
if response_discussions.status_code == 200:
    discussions = json.loads(response_discussions.text)
    for discussion in discussions:
        if discussion['is_announcement'] == False:
            print(f'Discussion Topic: {discussion["title"]}, Due: {discussion["due_at"]}')
else:
    print('Error: Failed to retrieve discussions topics.')
