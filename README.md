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

# Information

Thanks to Marten Gajda (http://dmfs.org/) for providing the first version, contributed to Birthday Adapter.

# How it is done
1. Copy current version of CalendarContract from Google's Android tree
2. Look at android.provider.Calendar from Android 2.2 how the fields are named there (http://grepcode.com/file/repository.grepcode.com/java/ext/com.google.android/android/2.2_r1.1/android/provider/Calendar.java)
3. Fix CalendarContract based on your findings