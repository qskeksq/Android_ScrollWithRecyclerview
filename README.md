# ScrollWithRecyclerview

- 리사이클러뷰와 같이 스크롤 가능한 레이아웃 설정

### 구조

- ConstraintLayout
    - CoordinatorLayout -> android:fitsSystemWindows="true"
        - AppBarLayout  -> android:fitsSystemWindows="true"
            - CollapsingToolbarLayout -> app:layout_scrollFlags="scroll|exitUntilCollapsed"
                - 리사이클러와 같이 스크롤될 레이아웃
                - 원래는 이름과 같이 Toolbar의 영역 -> app:layout_collapseMode="pin"
            - CollapsingToolbarLayout
        - AppBarLayout
        - Recyclervie ->  app:layout_behavior="@string/appbar_scrolling_view_behavior"
        - ListView계열을 사용하지 않는다면 NestedScrollView를 사용해야 함(ScrollView 불가) ->app:layout_behavior="@string/appbar_scrolling_view_behavior"
    - CoordinatorLayout
- ConstraintLayout

![](https://github.com/qskeksq/ScrollWithRecyclerview/blob/master/coordinatorlayout.PNG)

### 추가 설정
- CoordinatorLayout -> android:fitsSystemWindows="true"
- AppBarLayout  -> android:fitsSystemWindows="true"
- CollapsingToolbarLayout -> app:layout_scrollFlags="scroll|exitUntilCollapsed"
    - scroll : 스크롤 할 때 반응할 모든 뷰에 설정해야 한다. 설정하지 않으면 고정됨
    - enterAlways : 아래쪽 방향으로 스크롤 할 때마다 표시
    - exitUntilCollapsed : 해당 뷰에 minHeight가 설정되어 있으면 Toolbar나 설정된 레이아웃이 해당 크기까지만 축소
    - enterAlwaysCollapsed : 맨 위로 스크롤 될 때만 원래 크기로 확장
- Toolbar의 영역 -> app:layout_collapseMode="pin"
    - pin : CollapsingToolbarLayout이 완전히 축소되면 툴바는 화면위에 고정
    - parallax : 툴바가 축소되는 동안Parallax모드로 동작. 옵션으로 layout_collapseParallaxMultipler 속성을 사용하면 transition의 translation Multiplier를 설정할 수 있다.    
- Recyclervie ->  app:layout_behavior="@string/appbar_scrolling_view_behavior"
- NestedScrollView ->  app:layout_behavior="@string/appbar_scrolling_view_behavior"

```xml
<android.support.constraint.ConstraintLayout
    xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    xmlns:tools="http://schemas.android.com/tools"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:background="@android:color/white"
    android:clickable="true">

    <android.support.design.widget.CoordinatorLayout
        android:layout_width="0dp"
        android:layout_height="0dp"
        android:fitsSystemWindows="false"
        app:layout_constraintRight_toRightOf="parent"
        app:layout_constraintLeft_toLeftOf="parent"
        android:id="@+id/coordinatorLayout"
        app:layout_constraintBottom_toBottomOf="parent"
        app:layout_constraintHorizontal_bias="0.0"
        android:layout_marginBottom="0dp"
        app:layout_constraintTop_toTopOf="parent"
        android:layout_marginTop="0dp">

        <android.support.design.widget.AppBarLayout
            android:layout_width="match_parent"
            android:layout_height="170dp"
            android:background="@android:color/white"
            android:fitsSystemWindows="true">

            <android.support.design.widget.CollapsingToolbarLayout
                android:layout_width="match_parent"
                android:layout_height="match_parent"
                android:fitsSystemWindows="true"
                app:layout_scrollFlags="scroll|exitUntilCollapsed">

                <LinearLayout
                    android:layout_width="match_parent"
                    android:layout_height="match_parent"
                    android:orientation="vertical">

                    <android.support.v4.view.ViewPager
                        android:id="@+id/mainAdPager"
                        android:layout_width="match_parent"
                        android:layout_height="150dp"
                        android:layout_marginLeft="24dp"
                        android:layout_marginRight="24dp"
                        android:layout_marginTop="20dp"/>

                </LinearLayout>

            </android.support.design.widget.CollapsingToolbarLayout>

        </android.support.design.widget.AppBarLayout>

        <!--<android.support.v4.widget.NestedScrollView-->
            <!--android:layout_width="match_parent"-->
            <!--android:layout_height="match_parent"-->
            <!--app:layout_behavior="@string/appbar_scrolling_view_behavior">-->

            <android.support.v7.widget.RecyclerView
                android:id="@+id/homeRecycler"
                android:layout_width="match_parent"
                android:layout_height="wrap_content"
                app:layout_behavior="@string/appbar_scrolling_view_behavior" />

        <!--</android.support.v4.widget.NestedScrollView>-->

    </android.support.design.widget.CoordinatorLayout>

</android.support.constraint.ConstraintLayout>
```

http://freehoon.tistory.com/38 [초보 개발자] 참고