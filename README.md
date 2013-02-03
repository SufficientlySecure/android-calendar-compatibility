# Android ``CalendarContract`` class to support Android >= 2.2

CalendarContract class was introduced with Android 4.0 (ICS).
Older versions of Android are not supported officially.
This class enables the use of the calendar API from Android >= 2.2!

Put this Java file into your project to use it as a wrapper.
Pay attention to these issues:
* Not every field is supported on Android < 4. Test carefully!
* Some things need extra care on Android < 4!
When selecting calendars via query, setting your account in the by query parameters and the sync adapter query is not enough!
Also select them via query!

```Java
Uri calenderUri = Calendars.CONTENT_URI.buildUpon().appendQueryParameter(CalendarContract.CALLER_IS_SYNCADAPTER, "true")
                .appendQueryParameter(Calendars.ACCOUNT_NAME, myAccountName)
                .appendQueryParameter(Calendars.ACCOUNT_TYPE, myAccountType).build();
Cursor c1 = contentResolver.query(calenderUri, new String[] { BaseColumns._ID },
                Calendars.ACCOUNT_NAME + " = ? AND " + Calendars.ACCOUNT_TYPE + " = ?",
                new String[] { myAccountName, myAccountType }, null);
```

* Many more problems can occur!