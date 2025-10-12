#  2LEIC10T1 - Volut Development Report

Welcome to the Volut App documentation.

This Software Development Report, tailored for LEIC-ES-2024-25, provides comprehensive details about Volut, from high-level vision to low-level implementation decisions. It’s organised by the following activities.

Contributions are expected to be made exclusively by the initial team, but we may open them to the community, after the course, in all areas and topics: requirements, technologies, development, experimentation, testing, etc.

Please contact us!

Thank you!

- Afonso Saraiva up202304461@up.pt
- Ana Luís Carvalho up202307709@up.pt
- Guilherme Oliveira up202304717@up.pt
- Henrique Gonçalves up202307344@up.pt
- Rodrigo Rocha up202305891@up.pt


## Business Modelling 
Business modeling in software development involves defining the product's vision, understanding market needs, aligning features with user expectations, and setting the groundwork for strategic planning and execution.

### Product Vision

**Volut** is an app designed to help charity organizations easily publicize their events and recruit volunteers. The platform enables organizations to share upcoming events and opportunities, while volunteers can browse events, choose ones that align with their interests, and confirm their participation with a simple click.


## Requirements

### User Stories  

#### For Organizations:

##### Post Volunteer Opportunities  
_As a charity association, I want to post volunteer opportunities for upcoming events or actions, so that I can inform potential volunteers about our needs._  

##### Recruit Volunteers  
_As a charity association, I want to post volunteer opportunities for upcoming events or actions, so that I can find volunteers to help our cause._  

##### Showcase Organization Details  
_As a newly-founded volunteer association, we want to display our information so that it is easier to find us._  

#### For Volunteers:

##### Find Events Based on Interests  
_As a volunteer, I want to search for events happening on the weekends based on my interests, so that I can easily find opportunities to help where I am most needed._  

##### Access Organization Contacts  
_As a volunteer, I want to access the association contacts, so that I do not need to waste my time searching for them._  

##### Confirm Event Participation  
_As a volunteer, I want to log in to my account so that I can confirm my presence at an event._  


### Domain Modelling
Our app allows Users (Companies or Volunteers) to create accounts, letting Companies spread the word about their volunteering events and allowing Volunteers to find and participate in the volunteering opportunities they identify with the most.

- User-base class containing username, password and email, inherited by classes Volunteer and Company.
- Volunteer-stores information about user as well as the number of events participated.
- Company-contains information about the company.
- Opportunity-stores information about the event, its location and date.


<div align="center">
  <img src="img/Domainmodel.png">
</div>

## Architecture and Design

### Logical Architecture
This UML diagram represents the Logical View of the application. 
The **User Interface**, the front-end where users interact with the app, communicates with Business Logic to process user actions. **Business Logic** handles the main functionalities. This data is stored and retrieved in the **Data Access**.
The external system components such as the **Database (Firebase)**, which serves as the backend for data storage and retrieval ,and the **Google Maps API**, which is used for location-based features, provide functionality that the app does not handle internally.

<div align="center">
  <img src="img/logical.png">
</div>

 ### Physical Architecture
 
This is a Physical View diagram that illustrates how the app interacts with external services and storage. 
Users interact with the **Flutter App** on their devices. The app fetches event locations via **Google Maps API** and  while event-related data, such as upcoming events and volunteer sign-ups, is stored and managed via **Firebase**.
Additionally, some data is stored in **Local Storage** on the device to enhance performance ensuring a smoother user experience.

<div align="center">
  <img src="img/physical.png">
</div>

### UI Mockups

### Acceptance Tests

#### Feature: Post Events

  As a charity association,
  I want to post volunteer events for upcoming events or actions,
  So that I can find volunteers to help our cause.

    Scenario: Successfully post a new event
        Given I am logged in as a charity association
        When I navigate to the "My Events" page
        And I click on the "Post Event" button
        And I fill in the event details
            | Title       | Beach Cleanup Event       |
            | Description | Help us clean the beach   |
            | Date        | 2023-11-15                |
            | Location    | Santa Monica Beach        |
        And I submit the event
        Then I should see a confirmation message "Event posted successfully"
        And I should be redirected to the "My Events" page
        And the new event should be listed on the "Events" page

    Scenario: Fail to post a new event due to missing details
        Given I am logged in as a charity association
        When I naviagate to the "My Events" page
        And I click on the "Post Event" button
        And I fill in the event details
            | Title       | Beach Cleanup Event       |
            | Description |                           |
            | Date        | 2023-11-15                |
            | Location    | Santa Monica Beach        |
        And I submit the event
        Then I should see an error message "Description is required"
        And I should remain on the "Post Event" page
        And the new event should not be listed on the "Events" page

#### Feature: Access association contacts

  As a volunteer,
  I want to access the association contacts,
  So that I do not need to waste my time searching for them.

    Scenario: Volunteer accesses association contacts from a post
        Given I am a logged-in volunteer
        When I navigate to the organization's post
        Then I should see a list of association contacts
        And the list should include names, phone numbers, and email addresses

    Scenario: Volunteer accesses association contacts from the organization profile
        Given I am a logged-in volunteer
        When I navigate to the organization profile page
        Then I should see a list of association contacts
        And the list should include names, phone numbers, and email addresses


#### Feature: Display Association Information

  As a newly-founded volunteer association
  We want to display our information
  So that it is easier to find us

    Scenario: Display association information on the app
        Given An association posted a event
        When the user navigates trough the "Events" page
        And the user selects their event
        Then the app should display the association's name
        And the app should display the association's description
        And the app should display the association's contact information

#### Feature: User Login

  As a volunteer, 
  I want to login into my account 
  So that I can confirm my presence in an event.

    Scenario: Successful login
        Given I am a registered user
        And I am on the login page
        When I enter my valid username and password
        And I click the login button
        Then I should be redirected to the dashboard

    Scenario: Unsuccessful login with invalid credentials
        Given I am a registered user
        And I am on the login page
        When I enter an invalid username or password
        And I click the login button
        Then I should see an error message "Invalid username or password"

    Scenario: Unsuccessful login with empty fields
        Given I am a registered user
        And I am on the login page
        When I leave the username or password field empty
        And I click the login button
        Then I should see an error message "Username and password are required"

#### Feature: Search for weekend events based on interests

  As a volunteer,
  I want to search for events happening on the weekends based on my interests,
  So that I can easily find opportunities to help where I am most needed.

    Scenario: Search for weekend events by interest
        Given I am a registered volunteer
        And I am logged in
        When I enter my interests in the search bar
        And I select the option to filter events by weekends
        Then I should see a list of events happening on the weekends that match my interests

    Scenario: No events found for given interests
        Given I am a registered volunteer
        And I am logged in
        When I enter my interests in the search bar
        And I select the option to filter events by weekends
        Then I should see a message saying "No events found for your interests on the weekends"
## Backlog screenshots
### Print 1: Sprint 1 Start
![image](https://github.com/user-attachments/assets/5c92178f-8629-494b-b9fc-f81f9a0d8b2e)
  #### What is our SPRINT GOAL?
  In this sprint we intend to complete login authentication, be able to have a functional page to display the posts as well as the post creation.
  
### Print 2: Sprint 1 End
![image](https://github.com/user-attachments/assets/db5dbf7c-88b2-486f-aa09-ad44219c9980)
  #### What was done?
  We were able to implement part of the login authentication.
  
### Print 3: Sprint 2 Start
![image](https://github.com/user-attachments/assets/d827d301-3c5a-4390-9e4d-27a73bafb94c)
  #### What is our SPRINT GOAL?
   Finish login authentication with Firebase, post creation and display pages of the events in our app.

### Print 4: Sprint 2 End
![image](https://github.com/user-attachments/assets/431446a4-ea06-4e06-8723-bc9cba364ff9)
  #### What was done?
  We implemented login authentication with Firebase and did the "front-end" page of post creation.

### Print 5: Sprint 3 Start
![image](https://github.com/user-attachments/assets/f2fce1aa-f0f5-4610-b550-d9a87a005f6f)

  #### What is our SPRINT GOAL?
  We plan to add a database, complete every screen that is still missing and implement all the features still missing on the project.
  
### Print 6: Sprint 3 End
![image](https://github.com/user-attachments/assets/8e3549c7-f293-4688-bfb3-5946c5036d3f)
  #### What was done?
  We added the display of events in the fyp page, made small improvements in the login and sign up page, completed all the screens that were missing and the respective page navigation.
  
## Retrospective
### Sprint 1 Retrospective
In this sprint, the project's progress is not as good as we envisoned due to busy and incompatible post classes schedules and some technical problems with the Flutter emulators. To improve our dynamic, we plan to schedule weekly meetings to discuss and work on the project. We plan to catch up to our goals in the Easter's break.

### Sprint 2 Retrospective
In this sprint, the project's goal, although not fully completed as predicted, showed improvements. We did as much work as possible and discussed what would be our main focus having into acount the available time. The tasks we couldn't complete as planned were due to, as refered before, lack of time, mainly because of exams from other classes. Overall, we consider that int this sprint we managed to overcome a few of the isses relatively to the last sprint, making it a positive one. We plan to increase our efforts so that we can complete the project on time.

### Sprint 3 Retrospective
In this sprint, the project's progress toward completion was significant, with the only limitation being the available time. We worked collaboratively to achieve our goals and plan to complete any remaining tasks before pitch day. We believe this was clearly our best sprint so far, and we are committed to presenting our work effectively next week.

### Final Retrospective
Throughout the development of our project, we encountered some challenges—particularly with time management. One of the main issues was our difficulty in maintaining a steady, progressive workflow. Instead of distributing the workload evenly over the course of the project, we found ourselves needing to rush and stretch our efforts towards the end to complete everything on time.

Despite these setbacks, we believe the project was ultimately very rewarding and we are proud of our accomplishments. We managed to develop a solid application with a user-friendly interface, and we’re proud to say that it’s actually useful in day-to-day life. The experience taught us valuable lessons about planning and team coordination, and we’re satisfied with both the process and the final result.
