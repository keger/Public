package cn.dxy.android.a;

import android.content.Context;
import android.database.Cursor;
import android.database.sqlite.SQLiteDatabase;
import android.database.sqlite.SQLiteException;
import android.database.sqlite.SQLiteStatement;
import android.util.Log;
import cn.dxy.android.a.a.j;
import cn.dxy.android.a.a.m;
import cn.dxy.medicinehelper.MyApplication;
import java.io.File;
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class d
{
  private static d b = null;
  private static d c = null;
  private final String a = d.class.getName();
  private a d = null;
  private Context e = null;

  private d(Context paramContext)
  {
    this.e = paramContext;
    this.d = new a(paramContext);
  }

  private d(Context paramContext, a parama)
  {
    this.e = paramContext;
    this.d = parama;
  }

  public static d a(Context paramContext)
  {
    try
    {
      if (c == null)
        c = new d(paramContext, new c(paramContext));
      d locald = c;
      return locald;
    }
    finally
    {
    }
  }

  public static d b(Context paramContext)
  {
    try
    {
      if (b == null)
        b = new d(paramContext);
      for (d locald = b; ; locald = b)
        return locald;
    }
    finally
    {
    }
  }

  public int a(long paramLong1, long paramLong2, long paramLong3)
  {
    Cursor localCursor = null;
    SQLiteDatabase localSQLiteDatabase = a();
    try
    {
      localCursor = localSQLiteDatabase.rawQuery("select count(*) from guide_to_category where cateType=0 and cateId in (" + paramLong1 + "," + paramLong2 + "," + paramLong3 + ")", null);
      i = 0;
      if (localCursor != null)
      {
        boolean bool = localCursor.moveToLast();
        i = 0;
        if (bool)
        {
          int j = localCursor.getInt(0);
          i = j;
        }
      }
      return i;
    }
    catch (Throwable localThrowable)
    {
      Log.e(this.a, localThrowable.getMessage());
      int i = 0;
      return 0;
    }
    finally
    {
      if (localCursor != null)
        localCursor.close();
    }
  }

  public Cursor a(int paramInt)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString1 = { "id", "title", "size", "download", "magazine", "year" };
    String[] arrayOfString2 = new String[1];
    arrayOfString2[0] = ("%," + paramInt + ",%");
    return localSQLiteDatabase.query("guide", arrayOfString1, "diseaseIds LIKE ?", arrayOfString2, null, null, "createDate desc");
  }

  public Cursor a(long paramLong)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    if (paramLong == -1L)
      return localSQLiteDatabase.query("category", null, "supId is null AND id < 2000000", null, null, null, "position");
    return localSQLiteDatabase.query("category", null, "supId = " + paramLong + " AND id < 2000000", null, null, null, "position");
  }

  public Cursor a(long paramLong, int paramInt)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    boolean bool = paramLong < -1L;
    Cursor localCursor = null;
    if (bool)
    {
      String str = "SELECT id, showName, drugType FROM drug WHERE cateId1 = ? OR cateId2 = ? OR cateId3 = ? ORDER BY drugType ASC, position DESC limit 0," + (-1 + paramInt * 20);
      String[] arrayOfString = new String[3];
      arrayOfString[0] = ("" + paramLong);
      arrayOfString[1] = ("" + paramLong);
      arrayOfString[2] = ("" + paramLong);
      localCursor = localSQLiteDatabase.rawQuery(str, arrayOfString);
    }
    return localCursor;
  }

  public Cursor a(long paramLong, String paramString)
  {
    return a().query("drug_price a", null, "priceId = " + paramLong + " and standard = '" + paramString + "'", null, null, null, "a.date desc");
  }

  public Cursor a(String paramString, int paramInt)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    if (!Pattern.compile("[一-龥]").matcher(paramString).find())
    {
      String str2 = "SELECT id, showName, drugType FROM drug WHERE (shortName1 like ? OR shortName2 like ? OR shortName3 like ? ) ORDER BY drugType ASC, fullCnName ASC,position DESC limit 0," + (-1 + paramInt * 20);
      String[] arrayOfString2 = new String[3];
      arrayOfString2[0] = (paramString + "%");
      arrayOfString2[1] = (paramString + "%");
      arrayOfString2[2] = (paramString + "%");
      return localSQLiteDatabase.rawQuery(str2, arrayOfString2);
    }
    String str1 = "SELECT id, showName, drugType FROM drug WHERE (showName like ? OR otherName like ?) ORDER BY drugType ASC, fullCnName ASC,position DESC limit 0," + (-1 + paramInt * 20);
    String[] arrayOfString1 = new String[2];
    arrayOfString1[0] = ("%" + paramString + "%");
    arrayOfString1[1] = ("%|" + paramString + "|%");
    return localSQLiteDatabase.rawQuery(str1, arrayOfString1);
  }

  public Cursor a(String paramString1, String paramString2)
  {
    return a().rawQuery("SELECT actionId AS id, vsCnName1 AS name1, vsCnName2 AS showName FROM drug_to_action d WHERE vsEngName1 = ? AND vsEngName2 = ?", new String[] { paramString1, paramString2 });
  }

  public SQLiteDatabase a()
  {
    SQLiteDatabase localSQLiteDatabase = this.d.a();
    if (localSQLiteDatabase == null)
      throw new SQLiteException("Can NOT find any writable database.");
    return localSQLiteDatabase;
  }

  public String a(Cursor paramCursor, String paramString)
  {
    String str1 = "";
    if ((paramCursor != null) && (paramCursor.getPosition() >= 0) && (paramCursor.getPosition() < paramCursor.getCount()))
    {
      int i = paramCursor.getColumnIndex(paramString);
      if (i >= 0)
        str1 = paramCursor.getString(i);
    }
    if (cn.dxy.sso.e.a.c(str1))
    {
      str2 = str1.trim();
      if (!str2.endsWith("\\r"));
    }
    for (String str2 = str2.substring(0, str2.lastIndexOf("\\r")); ; str2 = "")
      return str2.trim();
  }

  public String a(String paramString)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    localSQLiteDatabase.beginTransaction();
    try
    {
      localSQLiteDatabase.execSQL(paramString);
      localSQLiteDatabase.setTransactionSuccessful();
      return "false";
    }
    catch (Exception localException)
    {
      String str = localException.getMessage();
      Log.e(this.a, str);
      return str;
    }
    finally
    {
      localSQLiteDatabase.endTransaction();
    }
  }

  public void a(long paramLong, boolean paramBoolean)
  {
    int i = 1;
    try
    {
      SQLiteDatabase localSQLiteDatabase = a();
      Object[] arrayOfObject = new Object[2];
      if (paramBoolean);
      while (true)
      {
        arrayOfObject[0] = Integer.valueOf(i);
        arrayOfObject[1] = Long.valueOf(paramLong);
        localSQLiteDatabase.execSQL(String.format("UPDATE guide SET download = %d WHERE id = %d;", arrayOfObject));
        return;
        i = 0;
      }
    }
    catch (Exception localException)
    {
      Log.e(this.a, "Error occurred " + localException.getMessage());
    }
  }

  public int b(long paramLong)
  {
    Cursor localCursor = a().rawQuery("SELECT count(*) FROM category WHERE supId = " + paramLong + " AND id < 2000000", null);
    localCursor.moveToFirst();
    int i = localCursor.getInt(0);
    localCursor.close();
    return i;
  }

  public int b(Cursor paramCursor, String paramString)
  {
    int i = -1;
    if ((paramCursor != null) && (paramCursor.getPosition() >= 0) && (paramCursor.getPosition() < paramCursor.getCount()))
    {
      int j = paramCursor.getColumnIndex(paramString);
      if (j >= 0)
        i = paramCursor.getInt(j);
    }
    return i;
  }

  public Cursor b(int paramInt)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString = new String[1];
    arrayOfString[0] = ("" + paramInt);
    return localSQLiteDatabase.rawQuery("SELECT * FROM drug_disease_therapy WHERE id = ?", arrayOfString);
  }

  public Cursor b(String paramString, int paramInt)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String str = "SELECT id, title, download, size,magazine,year FROM  guide WHERE title like ? OR summary like ? ORDER BY createDate DESC limit 0," + (-1 + paramInt * 20);
    String[] arrayOfString = new String[2];
    arrayOfString[0] = ("%" + paramString + "%");
    arrayOfString[1] = ("%" + paramString + "%");
    return localSQLiteDatabase.rawQuery(str, arrayOfString);
  }

  public Cursor b(String paramString1, String paramString2)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    if (paramString2.indexOf(",") > 0)
      return localSQLiteDatabase.rawQuery("SELECT * FROM drug WHERE innComponentId = ? and (routeId like '%,5,%' or routeId like '%,3,%') ORDER BY position DESC", new String[] { paramString1 });
    return localSQLiteDatabase.rawQuery("SELECT * FROM drug WHERE innComponentId = ? and routeId like '%,5,%' ORDER BY position DESC", new String[] { paramString1 });
  }

  public String b()
  {
    Cursor localCursor = null;
    SQLiteDatabase localSQLiteDatabase = a();
    Object localObject1 = "";
    try
    {
      localCursor = localSQLiteDatabase.rawQuery("SELECT * FROM version;", null);
      localCursor.moveToFirst();
      String str = localCursor.getString(localCursor.getColumnIndex("ver"));
      localObject1 = str;
      return localObject1;
    }
    catch (Exception localException)
    {
      Log.e(this.a, localException.getMessage());
      return localObject1;
    }
    finally
    {
      if (localCursor != null)
        localCursor.close();
    }
  }

  public String b(String paramString)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    localSQLiteDatabase.beginTransaction();
    while (true)
    {
      int j;
      try
      {
        String[] arrayOfString = paramString.replace(";;\r\n", ";;\n").split(";;\n");
        int i = arrayOfString.length;
        j = 0;
        if (j < i)
        {
          String str2 = arrayOfString[j];
          if (cn.dxy.sso.e.a.c(str2))
          {
            SQLiteStatement localSQLiteStatement = localSQLiteDatabase.compileStatement(str2);
            if (localSQLiteStatement != null)
              localSQLiteStatement.execute();
          }
        }
        else
        {
          localSQLiteDatabase.setTransactionSuccessful();
          return "false";
        }
      }
      catch (Exception localException)
      {
        String str1 = localException.getMessage();
        Log.e(this.a, str1);
        return str1;
      }
      finally
      {
        localSQLiteDatabase.endTransaction();
      }
      j++;
    }
  }

  public void b(long paramLong, boolean paramBoolean)
  {
    int i = 1;
    try
    {
      SQLiteDatabase localSQLiteDatabase = a();
      Object[] arrayOfObject = new Object[2];
      if (paramBoolean);
      while (true)
      {
        arrayOfObject[0] = Integer.valueOf(i);
        arrayOfObject[1] = Long.valueOf(paramLong);
        localSQLiteDatabase.execSQL(String.format("UPDATE clinical_pathway SET download = %d WHERE id = %d;", arrayOfObject));
        return;
        i = 0;
      }
    }
    catch (Exception localException)
    {
      Log.e(this.a, "Error occurred " + localException.getMessage());
    }
  }

  public int c(String paramString)
  {
    Cursor localCursor = a().rawQuery(String.format("SELECT id FROM category WHERE supId is not null AND (cnName='%s' or otherName like '%%|%s|%%') ORDER BY id ASC", new Object[] { paramString, paramString }), null);
    int i = -1;
    if (localCursor.getCount() > 0)
    {
      localCursor.moveToFirst();
      i = localCursor.getInt(localCursor.getColumnIndex("id"));
      localCursor.close();
    }
    return i;
  }

  public Cursor c()
  {
    return a().rawQuery("select id, cnName from guide_category order by shortName COLLATE LOCALIZED asc;", null);
  }

  public Cursor c(long paramLong)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    if (paramLong == -1L)
      return localSQLiteDatabase.query("category", null, "supId is null AND id > 2000000", null, null, null, "position");
    return localSQLiteDatabase.query("category", null, "supId = " + paramLong + " AND id > 2000000", null, null, null, "position");
  }

  public Cursor c(String paramString, int paramInt)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String str = "SELECT id, title,download,year FROM  clinical_pathway WHERE title like ? OR summary like ? ORDER BY createDate DESC limit 0," + (-1 + paramInt * 20);
    String[] arrayOfString = new String[2];
    arrayOfString[0] = ("%" + paramString + "%");
    arrayOfString[1] = ("%" + paramString + "%");
    return localSQLiteDatabase.rawQuery(str, arrayOfString);
  }

  public Long c(Cursor paramCursor, String paramString)
  {
    Long localLong = Long.valueOf(-1L);
    if ((paramCursor != null) && (paramCursor.getPosition() >= 0) && (paramCursor.getPosition() < paramCursor.getCount()))
    {
      int i = paramCursor.getColumnIndex(paramString);
      if (i >= 0)
        localLong = Long.valueOf(paramCursor.getLong(i));
    }
    return localLong;
  }

  public List c(int paramInt)
  {
    ArrayList localArrayList = new ArrayList();
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString = new String[1];
    arrayOfString[0] = ("" + paramInt);
    Cursor localCursor = localSQLiteDatabase.rawQuery("SELECT * FROM relation_disease_component WHERE component_id <>'' AND component_name <>'' AND disease_id = ? order by priority desc", arrayOfString);
    while (true)
      if (localCursor.moveToNext())
      {
        String str = a(localCursor, "component_id");
        if (str.length() > 3)
          str = str.substring(1, -2 + str.length());
        cn.dxy.android.medicinehelper.a.a.c localc = new cn.dxy.android.medicinehelper.a.a.c();
        try
        {
          localc.a = new String(cn.dxy.sso.e.c.b(a(localCursor, "component_name")), "utf-8");
          localc.b = str;
          localc.c = a(localCursor, "route_id");
          localArrayList.add(localc);
        }
        catch (Exception localException)
        {
          while (true)
            localException.printStackTrace();
        }
      }
    localCursor.close();
    return localArrayList;
  }

  public int d(long paramLong)
  {
    Cursor localCursor = a().rawQuery("SELECT count(*) FROM category WHERE supId = " + paramLong + " AND id > 2000000", null);
    localCursor.moveToFirst();
    int i = localCursor.getInt(0);
    localCursor.close();
    return i;
  }

  public Cursor d()
  {
    return a().rawQuery("select id, cateName from clinical_pathway_category order by position asc;", null);
  }

  public Cursor d(String paramString)
  {
    Log.e("category ID", paramString);
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString = new String[2];
    arrayOfString[0] = ("%," + paramString);
    arrayOfString[1] = paramString;
    return localSQLiteDatabase.rawQuery("SELECT * FROM drug WHERE innComponentId like ? or innComponentId like ? ORDER BY drugType ASC, shortName1 ASC,position ASC;", arrayOfString);
  }

  public Cursor d(String paramString, int paramInt)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    if (!Pattern.compile("[一-龥]").matcher(paramString).find())
    {
      String str2 = "SELECT id, showName, vsName, drugType FROM drug WHERE  ( vsName!='' AND (shortName1 like ? OR shortName2 like ? OR shortName3 like ?) ) ORDER BY drugType ASC, shortName1 ASC,position ASC limit 0," + (-1 + paramInt * 20);
      String[] arrayOfString2 = new String[3];
      arrayOfString2[0] = (paramString + "%");
      arrayOfString2[1] = (paramString + "%");
      arrayOfString2[2] = (paramString + "%");
      return localSQLiteDatabase.rawQuery(str2, arrayOfString2);
    }
    String str1 = "SELECT id, showName, vsName, drugType FROM drug WHERE  ( vsName!='' AND showName like ? ) ORDER BY drugType ASC, shortName1 ASC,position ASC limit 0," + (-1 + paramInt * 20);
    String[] arrayOfString1 = new String[1];
    arrayOfString1[0] = ("%" + paramString + "%");
    return localSQLiteDatabase.rawQuery(str1, arrayOfString1);
  }

  public int e(long paramLong)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    boolean bool = paramLong < -1L;
    Cursor localCursor = null;
    if (bool)
    {
      String[] arrayOfString = new String[3];
      arrayOfString[0] = ("" + paramLong);
      arrayOfString[1] = ("" + paramLong);
      arrayOfString[2] = ("" + paramLong);
      localCursor = localSQLiteDatabase.rawQuery("SELECT count(*) FROM drug WHERE cateId1 = ? OR cateId2 = ? OR cateId3 = ? ", arrayOfString);
    }
    localCursor.moveToFirst();
    int i = localCursor.getInt(0);
    localCursor.close();
    return i;
  }

  public int e(String paramString)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString2;
    if (!Pattern.compile("[一-龥]").matcher(paramString).find())
    {
      arrayOfString2 = new String[3];
      arrayOfString2[0] = (paramString + "%");
      arrayOfString2[1] = (paramString + "%");
      arrayOfString2[2] = (paramString + "%");
    }
    String[] arrayOfString1;
    for (Cursor localCursor = localSQLiteDatabase.rawQuery("SELECT count(*) FROM drug WHERE (shortName1 like ? OR shortName2 like ? OR shortName3 like ? ) ", arrayOfString2); ; localCursor = localSQLiteDatabase.rawQuery("SELECT count(*) FROM drug WHERE (showName like ? ) ", arrayOfString1))
    {
      localCursor.moveToFirst();
      int i = localCursor.getInt(0);
      localCursor.close();
      return i;
      arrayOfString1 = new String[1];
      arrayOfString1[0] = ("%" + paramString + "%");
    }
  }

  public Cursor e()
  {
    SQLiteDatabase localSQLiteDatabase = a();
    StringBuilder localStringBuilder = new StringBuilder("(");
    for (String str1 : new File(MyApplication.m()).list())
      if ((str1.startsWith("guide_")) && (str1.endsWith(".json")))
      {
        String str2 = str1.substring(1 + str1.indexOf('_'), str1.indexOf('.'));
        localStringBuilder.append(str2 + ",");
      }
    localStringBuilder.replace(-1 + localStringBuilder.length(), localStringBuilder.length(), ")");
    if (localStringBuilder.length() > 1)
    {
      localStringBuilder.replace(-1 + localStringBuilder.length(), localStringBuilder.length(), ")");
      return localSQLiteDatabase.rawQuery("SELECT * FROM guide WHERE id in " + localStringBuilder, null);
    }
    return localSQLiteDatabase.rawQuery("SELECT * FROM guide WHERE id in ()", null);
  }

  public Cursor e(String paramString, int paramInt)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String str = "SELECT DISTINCT(search.drugId) AS id, search.showName, search.drugType FROM drug_search search,drug drug WHERE search.drugId = drug.id AND (search.searchWord like ?) AND  ( search.type = 1 OR search.type = 3) ORDER BY drug.drugType ASC,drug.position DESC,drug.fullCnName ASC limit 0," + (-1 + paramInt * 20);
    String[] arrayOfString = new String[1];
    arrayOfString[0] = (paramString + "%");
    return localSQLiteDatabase.rawQuery(str, arrayOfString);
  }

  public int f(String paramString)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString = new String[2];
    arrayOfString[0] = ("%" + paramString + "%");
    arrayOfString[1] = ("%" + paramString + "%");
    Cursor localCursor = localSQLiteDatabase.rawQuery("SELECT count(*) FROM  guide WHERE title like ? OR summary like ? ", arrayOfString);
    localCursor.moveToFirst();
    int i = localCursor.getInt(0);
    localCursor.close();
    return i;
  }

  public Cursor f()
  {
    SQLiteDatabase localSQLiteDatabase = a();
    StringBuilder localStringBuilder = new StringBuilder("(");
    for (String str1 : new File(MyApplication.m()).list())
      if ((str1.startsWith("pathway_")) && (str1.endsWith(".json")))
      {
        String str2 = str1.substring(1 + str1.indexOf('_'), str1.indexOf('.'));
        localStringBuilder.append(str2 + ",");
      }
    if (localStringBuilder.length() > 1)
    {
      localStringBuilder.replace(-1 + localStringBuilder.length(), localStringBuilder.length(), ")");
      return localSQLiteDatabase.rawQuery("SELECT * FROM clinical_pathway WHERE id in " + localStringBuilder, null);
    }
    return localSQLiteDatabase.rawQuery("SELECT * FROM clinical_pathway WHERE id in ()", null);
  }

  public Cursor f(long paramLong)
  {
    return a().query("drug", null, "id = " + paramLong, null, null, null, null);
  }

  public Cursor f(String paramString, int paramInt)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String str = "select id, word AS showName, 0 as drugType from search_tip WHERE (pinyin like ?) ORDER BY showName COLLATE LOCALIZED DESC limit 0," + (-1 + paramInt * 20);
    String[] arrayOfString = new String[1];
    arrayOfString[0] = (paramString + "%");
    return localSQLiteDatabase.rawQuery(str, arrayOfString);
  }

  public int g(String paramString)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString = new String[2];
    arrayOfString[0] = ("%" + paramString + "%");
    arrayOfString[1] = ("%" + paramString + "%");
    Cursor localCursor = localSQLiteDatabase.rawQuery("SELECT count(*) FROM  clinical_pathway WHERE title like ? OR summary like ?", arrayOfString);
    localCursor.moveToFirst();
    int i = localCursor.getInt(0);
    localCursor.close();
    return i;
  }

  public Cursor g(long paramLong)
  {
    return a().query("drug_price a", null, "priceId = " + paramLong, null, null, null, "a.date desc");
  }

  public Cursor g(String paramString, int paramInt)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String str = "SELECT DISTINCT(drugId) AS id, showName, drugType FROM drug_search WHERE  (searchWord like ?) AND type = 2 ORDER BY showName COLLATE LOCALIZED DESC, searchWord DESC limit 0," + (-1 + paramInt * 20);
    String[] arrayOfString = new String[1];
    arrayOfString[0] = (paramString + "%");
    return localSQLiteDatabase.rawQuery(str, arrayOfString);
  }

  public void g()
  {
    if (b != null)
    {
      this.d.b();
      b = null;
    }
  }

  public int h(String paramString)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString2;
    if (!Pattern.compile("[一-龥]").matcher(paramString).find())
    {
      arrayOfString2 = new String[3];
      arrayOfString2[0] = (paramString + "%");
      arrayOfString2[1] = (paramString + "%");
      arrayOfString2[2] = (paramString + "%");
    }
    String[] arrayOfString1;
    for (Cursor localCursor = localSQLiteDatabase.rawQuery("SELECT count(*) FROM drug WHERE  ( vsName!='' AND (shortName1 like ? OR shortName2 like ? OR shortName3 like ?) )", arrayOfString2); ; localCursor = localSQLiteDatabase.rawQuery("SELECT count(*) FROM drug WHERE  ( vsName!='' AND showName like ? ) ", arrayOfString1))
    {
      localCursor.moveToFirst();
      int i = localCursor.getInt(0);
      localCursor.close();
      return i;
      arrayOfString1 = new String[1];
      arrayOfString1[0] = ("%" + paramString + "%");
    }
  }

  public Cursor h(String paramString, int paramInt)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String str = "SELECT * FROM drug_disease_therapy where disease_name_cn like ?  or disease_name_entry_cn like ? or disease_abbreviation_cn like ?  or wrong_writen like ? limit 0," + (-1 + paramInt * 20);
    String[] arrayOfString = new String[1];
    arrayOfString[0] = ("%" + paramString + "%");
    return localSQLiteDatabase.rawQuery(str, arrayOfString);
  }

  public void h()
  {
    if (c != null)
    {
      this.d.b();
      c = null;
    }
  }

  public boolean h(long paramLong)
  {
    Cursor localCursor = a().query("drug", null, "id = " + paramLong + " and status < 100", null, null, null, null);
    if ((localCursor != null) && (localCursor.getCount() > 0));
    for (boolean bool = true; ; bool = false)
    {
      localCursor.close();
      return bool;
    }
  }

  public Cursor i(String paramString)
  {
    return a().rawQuery("SELECT actionId AS id, vsCnName1 AS name1, vsCnName2 AS showName FROM drug_to_action d WHERE vsEngName1 = ? OR vsEngName2 = ?", new String[] { paramString, paramString });
  }

  public boolean i(long paramLong)
  {
    Cursor localCursor = a().query("guide a", null, "id = " + paramLong + " and deleted = 0", null, null, null, "a.title");
    if ((localCursor != null) && (localCursor.getCount() > 0));
    for (boolean bool = true; ; bool = false)
    {
      localCursor.close();
      return bool;
    }
  }

  public Cursor j(long paramLong)
  {
    return a().query("drug_prop_" + paramLong % 10L + " a, drug_field b", new String[] { "b.cnName", "b.engName", "a.value" }, "a.fieldId = b.id AND a.drugId = " + paramLong, null, null, null, "position");
  }

  public void j(String paramString)
  {
    Cursor localCursor = null;
    SQLiteDatabase localSQLiteDatabase = a();
    try
    {
      boolean bool = cn.dxy.sso.e.a.c(paramString);
      localCursor = null;
      if (bool)
      {
        if (paramString.endsWith(","))
          paramString.substring(0, -1 + paramString.length());
        localCursor = localSQLiteDatabase.rawQuery("select id, showName from drug where id in(" + paramString + ");", null);
        if (localCursor != null)
          MyApplication.f.a(localCursor);
      }
      return;
    }
    catch (Throwable localThrowable)
    {
      Log.e(this.a, localThrowable.getMessage());
      return;
    }
    finally
    {
      if (localCursor != null)
        localCursor.close();
    }
  }

  public String k(long paramLong)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString1 = { "vsName" };
    String[] arrayOfString2 = new String[1];
    arrayOfString2[0] = String.valueOf(paramLong);
    Cursor localCursor = localSQLiteDatabase.query("drug", arrayOfString1, "id=?", arrayOfString2, null, null, null);
    boolean bool = localCursor.moveToFirst();
    String str = null;
    if (bool)
      str = a(localCursor, "vsName");
    return str;
  }

  public void k(String paramString)
  {
    Cursor localCursor = null;
    SQLiteDatabase localSQLiteDatabase = a();
    try
    {
      boolean bool = cn.dxy.sso.e.a.c(paramString);
      localCursor = null;
      if (bool)
      {
        if (paramString.endsWith(","))
          paramString.substring(0, -1 + paramString.length());
        localCursor = localSQLiteDatabase.rawQuery("select id,title from guide where id in(" + paramString + ");", null);
        if (localCursor != null)
          MyApplication.g.a(localCursor);
      }
      return;
    }
    catch (Throwable localThrowable)
    {
      Log.e(this.a, localThrowable.getMessage());
      return;
    }
    finally
    {
      if (localCursor != null)
        localCursor.close();
    }
  }

  public Cursor l(long paramLong)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString = new String[1];
    arrayOfString[0] = ("" + paramLong);
    return localSQLiteDatabase.rawQuery("SELECT * FROM drug_action WHERE id = ?", arrayOfString);
  }

  public Cursor l(String paramString)
  {
    return a().query("guide a, guide_to_category b", new String[] { "a.id", "a.title", "a.size", "a.download", "a.magazine", "a.year" }, "a.id = b.guideId and b.cateType=0 and b.cateId in (" + paramString + ")", null, null, null, "a.createDate desc");
  }

  public String m(long paramLong)
  {
    String str = "";
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString = new String[1];
    arrayOfString[0] = ("" + paramLong);
    Cursor localCursor = localSQLiteDatabase.rawQuery("SELECT cnName FROM company WHERE id = ?", arrayOfString);
    if (localCursor.moveToNext())
      str = localCursor.getString(0);
    localCursor.close();
    return str;
  }

  public void m(String paramString)
  {
    Cursor localCursor = null;
    SQLiteDatabase localSQLiteDatabase = a();
    try
    {
      boolean bool = cn.dxy.sso.e.a.c(paramString);
      localCursor = null;
      if (bool)
      {
        if (paramString.endsWith(","))
          paramString.substring(0, -1 + paramString.length());
        localCursor = localSQLiteDatabase.rawQuery("select id,title from clinical_pathway where id in(" + paramString + ");", null);
        if (localCursor != null)
          MyApplication.h.a(localCursor);
      }
      return;
    }
    catch (Throwable localThrowable)
    {
      Log.e(this.a, localThrowable.getMessage());
      return;
    }
    finally
    {
      if (localCursor != null)
        localCursor.close();
    }
  }

  public int n(String paramString)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString = new String[1];
    arrayOfString[0] = (paramString + "%");
    Cursor localCursor = localSQLiteDatabase.rawQuery("SELECT count(*) FROM drug_search WHERE  (searchWord like ?) AND  ( type = 1 OR type = 3)", arrayOfString);
    localCursor.moveToFirst();
    int i = localCursor.getInt(0);
    localCursor.close();
    return i;
  }

  public long n(long paramLong)
  {
    long l = -1L;
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString = new String[1];
    arrayOfString[0] = ("" + paramLong);
    Cursor localCursor = localSQLiteDatabase.rawQuery("SELECT companyId FROM drug WHERE id = ?", arrayOfString);
    if (localCursor.moveToNext())
      l = localCursor.getLong(0);
    localCursor.close();
    return l;
  }

  public int o(long paramLong)
  {
    Cursor localCursor = a().query("guide a, guide_to_category b", new String[] { "count(*)" }, "a.id = b.guideId and b.cateType=1 and a.size>0 and b.cateId = " + paramLong, null, null, null, null);
    localCursor.moveToFirst();
    int i = localCursor.getInt(0);
    localCursor.close();
    return i;
  }

  public int o(String paramString)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString = new String[1];
    arrayOfString[0] = (paramString + "%");
    Cursor localCursor = localSQLiteDatabase.rawQuery("select count(*) from search_tip WHERE (pinyin like ?) ", arrayOfString);
    localCursor.moveToFirst();
    int i = localCursor.getInt(0);
    localCursor.close();
    return i;
  }

  public int p(String paramString)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString = new String[1];
    arrayOfString[0] = (paramString + "%");
    Cursor localCursor = localSQLiteDatabase.rawQuery("SELECT DISTINCT(drugId) AS id, showName, drugType FROM drug_search WHERE  (searchWord like ?) AND type = 2", arrayOfString);
    int i = localCursor.getCount();
    localCursor.close();
    return i;
  }

  public Cursor p(long paramLong)
  {
    return a().query("guide a, guide_to_category b", new String[] { "a.id", "a.title", "a.size", "a.download", "a.magazine", "a.year" }, "a.id = b.guideId and b.cateType=1 and a.size>0 and b.cateId = " + paramLong, null, null, null, "a.createDate desc");
  }

  public Cursor q(long paramLong)
  {
    return a().query("guide a", null, "id = " + paramLong, null, null, null, "a.title");
  }

  public Cursor q(String paramString)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    if (cn.dxy.sso.e.a.b(paramString))
      return localSQLiteDatabase.rawQuery("SELECT * FROM drug_disease_therapy where isIndex = 1 order by priority desc", null);
    return localSQLiteDatabase.rawQuery("SELECT * FROM drug_disease_therapy where isIndex is NULL and ancestor_id like '%," + paramString + ",%' order by priority desc limit 0,10", null);
  }

  public int r(String paramString)
  {
    SQLiteDatabase localSQLiteDatabase = a();
    String[] arrayOfString = new String[1];
    arrayOfString[0] = ("%" + paramString + "%");
    Cursor localCursor = localSQLiteDatabase.rawQuery("SELECT count(*) FROM drug_disease_therapy where disease_name_cn like ? or disease_name_entry_cn like ? or disease_abbreviation_cn like ?  or wrong_writen like ?", arrayOfString);
    localCursor.moveToFirst();
    int i = localCursor.getInt(0);
    localCursor.close();
    return i;
  }

  public long r(long paramLong)
  {
    long l1 = 0L;
    Cursor localCursor = null;
    SQLiteDatabase localSQLiteDatabase = a();
    try
    {
      Object[] arrayOfObject = new Object[1];
      arrayOfObject[0] = Long.valueOf(paramLong);
      localCursor = localSQLiteDatabase.rawQuery(String.format("SELECT modifyDate FROM guide WHERE id = %d;", arrayOfObject), null);
      localCursor.moveToFirst();
      SimpleDateFormat localSimpleDateFormat = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
      String str = localCursor.getString(localCursor.getColumnIndex("modifyDate"));
      boolean bool = cn.dxy.sso.e.a.b(str);
      if (bool);
      while (true)
      {
        return l1;
        long l2 = localSimpleDateFormat.parse(str).getTime();
        l1 = l2;
      }
    }
    catch (Throwable localThrowable)
    {
      Log.e(this.a, localThrowable.getMessage());
      return l1;
    }
    finally
    {
      if (localCursor != null)
        localCursor.close();
    }
  }

  public int s(long paramLong)
  {
    Cursor localCursor = a().query("clinical_pathway a, clinical_pathway_to_category b", new String[] { "count(*)" }, "a.id = b.pathwayId and b.cateType=2 and b.cateId = " + paramLong, null, null, null, null);
    localCursor.moveToFirst();
    int i = localCursor.getInt(0);
    localCursor.close();
    return i;
  }

  public Cursor s(String paramString)
  {
    return a().rawQuery("SELECT * FROM drug WHERE innComponentId = ? ORDER BY position DESC", new String[] { paramString });
  }

  public Cursor t(long paramLong)
  {
    return a().query("clinical_pathway a, clinical_pathway_to_category b", new String[] { "a.id", "a.title", "a.download", "a.year" }, "a.id = b.pathwayId and b.cateType=2 and b.cateId = " + paramLong, null, null, null, "a.createDate desc");
  }

  public Cursor u(long paramLong)
  {
    return a().query("clinical_pathway a", null, "id = " + paramLong, null, null, null, "a.title");
  }

  public long v(long paramLong)
  {
    long l1 = 0L;
    Cursor localCursor = null;
    SQLiteDatabase localSQLiteDatabase = a();
    try
    {
      Object[] arrayOfObject = new Object[1];
      arrayOfObject[0] = Long.valueOf(paramLong);
      localCursor = localSQLiteDatabase.rawQuery(String.format("SELECT modifyDate FROM clinical_pathway WHERE id = %d;", arrayOfObject), null);
      localCursor.moveToFirst();
      SimpleDateFormat localSimpleDateFormat = new SimpleDateFormat("yyyy-MM-dd hh:mm:ss");
      String str = localCursor.getString(localCursor.getColumnIndex("modifyDate"));
      boolean bool = cn.dxy.sso.e.a.b(str);
      if (bool);
      while (true)
      {
        return l1;
        long l2 = localSimpleDateFormat.parse(str).getTime();
        l1 = l2;
      }
    }
    catch (Throwable localThrowable)
    {
      Log.e(this.a, localThrowable.getMessage());
      return l1;
    }
    finally
    {
      if (localCursor != null)
        localCursor.close();
    }
  }
}
