# EnumIndexer

Enum 개수만큼 Object생성 Enum으로 객체 접근

## Code
```C#
public class EnumIndexer<T>
{
    T[] values;

    public EnumIndexer(Type enumType)
    {
        values = new T[Enum.GetNames(enumType).Length];
    }

    public int Length => values.Length;

    public T this[int index]
    {
        get => values[(int)index];
        set => values[(int)index] = value;
    }

    public T this[Enum index]
    {
        get => values[Convert.ToInt32(index)];
        set => values[Convert.ToInt32(index)] = value;
    }
}
```

## Example
```C#
enum EElement
{
    Code,
    LoginId,
    Password
}

EnumIndexer<ElementReference> Element { get; set; } = new EnumIndexer<ElementReference>(typeof(EElement));

...
{
    if (requestObject.Message.IndexOf("PassWord") != -1)
        await Element[EElement.Password].FocusAsync();
    else if (requestObject.Message.IndexOf("ID") != -1)
        await Element[EElement.LoginId].FocusAsync();
    else
        await Element[EElement.Code].FocusAsync();
}
```

