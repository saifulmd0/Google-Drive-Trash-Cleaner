# Google-Drive-Trash-Cleaner
Clean your Google Drive trash automatically based on a set schedule 

You can automate the process of cleaning the trash in Google Drive using Google Apps Script. Google Apps Script is a scripting platform developed by Google for light-weight application development in the G Suite platform. Here's a step-by-step guide on how to create a script that will empty the trash daily:

## Open Google Apps Script:

**1. Go to Google Apps Script.**
- Click on "New project".

**2. Write the Script:**
- Copy and paste the following script into the script editor:

```
function emptyTrash() {
  // Delete trashed files
  var trashFiles = DriveApp.getTrashedFiles();
  while (trashFiles.hasNext()) {
    var file = trashFiles.next();
    file.setTrashed(false); // Restore the file
    Drive.Files.remove(file.getId()); // Permanently delete the file
  }

  // Delete trashed folders
  var trashFolders = DriveApp.getTrashedFolders();
  while (trashFolders.hasNext()) {
    var folder = trashFolders.next();
    folder.setTrashed(false); // Restore the folder
    Drive.Files.remove(folder.getId()); // Permanently delete the folder
  }
}

```

**3.Enable Drive API:**
- Click on Services in the left-hand menu.
- Click on the + button at the bottom right.
- Find Drive API in the list and enable it.


## Enable Google Drive API in Google Cloud Console

**1. Open Google Cloud Console:**
- Go to Google Cloud Console.
- Select your project (or create a new one if necessary).

**2. Enable API:**
- Navigate to APIs & Services > Library.
- Search for Google Drive API and enable it.

**3. Set up a Trigger:**
- Click on the clock icon in the toolbar to open the "Triggers" page.
- Click on "Add Trigger" at the bottom right.
- Set the function to emptyTrash, the deployment to Head, and the event source to Time-driven.
- Choose "Day timer" and select a specific time for the script to run daily.
- Save the trigger.

## Finally Run the script

**1. Authorize the Script:**
When you run the script for the first time, it will ask for authorization.
Review the permissions and authorize the script to access your Google Drive.
By following these steps, the script will run daily at the specified time and empty the trash in your Google Drive automatically.

Thanks.
