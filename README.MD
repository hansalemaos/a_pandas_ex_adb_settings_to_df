# Parses all Android config files (json/db/xml) in the /data/ folder and returns an easy-to-handle DataFrame

### Some things you have to know:

- You need root access 
- I have only tested it against BlueStacks / Windows 10 / Python 3.9.
- The parsing might take a while and the DataFrame might get huge. (103,000 rows on my BlueStacks emulator with 3 apps installed [Roblox, YouTube, GloboTV]
- It ignores all Exceptions, but prints them out. Usually, you can ignore them because, most of the time, they are thrown because of empty files 
- Don't use the sed columns yet (search and replace) on a real device. You could screw up your cell phone. 



```python

$pip install a-pandas-ex-adb-settings-to-df

from a_pandas_ex_adb_settings_to_df import pd_add_adb_settings_to_df
pd_add_adb_settings_to_df()
import pandas as pd
adb_path = "C:\\Users\\Gamer\\AppData\\Local\\Android\\Sdk\\platform-tools\\adb.exe"
deviceserial = "localhost:5875"
save_in_folder = "f:\\tempfilesforandroid" # to save the json/db/xml files
df = pd.Q_adb_settings_to_df(
    adb_path=adb_path,
    deviceserial=deviceserial,
    save_in_folder=save_in_folder,
    folder="data/", # Should be the same on any android device,
	with_sed_columns=False # DON'T USE THIS ON A REAL DEVICE! SEARCH + REPLACE 
)



        index          aa_all_keys  ... level_6 level_7
0         0.0         (long, name)  ...     NaN     NaN
1         1.0        (long, value)  ...     NaN     NaN
2         0.0   (boolean, 0, name)  ...     NaN     NaN
3         1.0  (boolean, 0, value)  ...     NaN     NaN
4         2.0   (boolean, 1, name)  ...     NaN     NaN
       ...                  ...  ...     ...     ...
103404    NaN            (6, desc)  ...     NaN     NaN
103405    NaN           (6, label)  ...     NaN     NaN
103406    NaN             (6, pkg)  ...     NaN     NaN
103407    NaN          (6, source)  ...     NaN     NaN
103408    NaN             (6, url)  ...     NaN     NaN
[103409 rows x 15 columns]


print(df[10:20].to_string())
    index          aa_all_keys                                      aa_value      aa_xpath                                                    aa_snippet                                                                                                  aa_file                                                                    aa_file_android  level_0 level_1 level_2 level_3 level_4 level_5 level_6 level_7
10    8.0   (boolean, 4, name)                   preferences_home_tz_enabled  //boolean[5]   <boolean name="preferences_home_tz_enabled" value="false"/>  f:\tempfilesforandroid\data\data\com.android.calendar\shared_prefs\com.android.calendar_preferences.xml  /data/data/com.android.calendar/shared_prefs/com.android.calendar_preferences.xml  boolean       4    name    <NA>    <NA>    <NA>    <NA>    <NA>
11    9.0  (boolean, 4, value)                                         false  //boolean[5]   <boolean name="preferences_home_tz_enabled" value="false"/>  f:\tempfilesforandroid\data\data\com.android.calendar\shared_prefs\com.android.calendar_preferences.xml  /data/data/com.android.calendar/shared_prefs/com.android.calendar_preferences.xml  boolean       4   value    <NA>    <NA>    <NA>    <NA>    <NA>
12   10.0   (boolean, 5, name)                      preferences_alerts_popup  //boolean[6]      <boolean name="preferences_alerts_popup" value="false"/>  f:\tempfilesforandroid\data\data\com.android.calendar\shared_prefs\com.android.calendar_preferences.xml  /data/data/com.android.calendar/shared_prefs/com.android.calendar_preferences.xml  boolean       5    name    <NA>    <NA>    <NA>    <NA>    <NA>
13   11.0  (boolean, 5, value)                                         false  //boolean[6]      <boolean name="preferences_alerts_popup" value="false"/>  f:\tempfilesforandroid\data\data\com.android.calendar\shared_prefs\com.android.calendar_preferences.xml  /data/data/com.android.calendar/shared_prefs/com.android.calendar_preferences.xml  boolean       5   value    <NA>    <NA>    <NA>    <NA>    <NA>
14   12.0    (string, 0, name)                    preferences_week_start_day   //string[1]                    <string name="preferences_week_start_day">  f:\tempfilesforandroid\data\data\com.android.calendar\shared_prefs\com.android.calendar_preferences.xml  /data/data/com.android.calendar/shared_prefs/com.android.calendar_preferences.xml   string       0    name    <NA>    <NA>    <NA>    <NA>    <NA>
15   13.0  (string, 0, string)                                            -1   //string[1]                    <string name="preferences_week_start_day">  f:\tempfilesforandroid\data\data\com.android.calendar\shared_prefs\com.android.calendar_preferences.xml  /data/data/com.android.calendar/shared_prefs/com.android.calendar_preferences.xml   string       0  string    <NA>    <NA>    <NA>    <NA>    <NA>
16   14.0    (string, 1, name)                           preferences_version   //string[2]                           <string name="preferences_version">  f:\tempfilesforandroid\data\data\com.android.calendar\shared_prefs\com.android.calendar_preferences.xml  /data/data/com.android.calendar/shared_prefs/com.android.calendar_preferences.xml   string       1    name    <NA>    <NA>    <NA>    <NA>    <NA>
17   15.0  (string, 1, string)                                         7.1.2   //string[2]                           <string name="preferences_version">  f:\tempfilesforandroid\data\data\com.android.calendar\shared_prefs\com.android.calendar_preferences.xml  /data/data/com.android.calendar/shared_prefs/com.android.calendar_preferences.xml   string       1  string    <NA>    <NA>    <NA>    <NA>    <NA>
18   16.0    (string, 2, name)                   preferences_alerts_ringtone   //string[3]                   <string name="preferences_alerts_ringtone">  f:\tempfilesforandroid\data\data\com.android.calendar\shared_prefs\com.android.calendar_preferences.xml  /data/data/com.android.calendar/shared_prefs/com.android.calendar_preferences.xml   string       2    name    <NA>    <NA>    <NA>    <NA>    <NA>
19   17.0  (string, 2, string)  content://settings/system/notification_sound   //string[3]                   <string name="preferences_alerts_ringtone">  f:\tempfilesforandroid\data\data\com.android.calendar\shared_prefs\com.android.calendar_preferences.xml  /data/data/com.android.calendar/shared_prefs/com.android.calendar_preferences.xml   string       2  string    <NA>    <NA>    <NA>    <NA>    <NA>


```
