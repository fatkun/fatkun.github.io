---
title: Android ViewHolder模式
author: fatkun
type: post
date: 2012-01-07T07:46:54+00:00
url: /2012/01/android-viewholder.html
duoshuo_thread_id:
  - 6300408827548271361
wp-syntax-cache-content:
  - |
    a:2:{i:1;s:673:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;">        <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">class</span> ViewHolder <span style="color: #009900;">&#123;</span>
                TextView text<span style="color: #339933;">;</span>
                ImageView icon<span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">        static class ViewHolder {
                TextView text;
                ImageView icon;
            }</p></div>
    ";i:2;s:22069:"
    <div class="wp_syntax" style="position:relative;"><table><tr><td class="code"><pre class="java" style="font-family:monospace;"><span style="color: #666666; font-style: italic;">/*
     * Copyright (C) 2008 The Android Open Source Project
     *
     * Licensed under the Apache License, Version 2.0 (the &quot;License&quot;);
     * you may not use this file except in compliance with the License.
     * You may obtain a copy of the License at
     *
     *      http://www.apache.org/licenses/LICENSE-2.0
     *
     * Unless required by applicable law or agreed to in writing, software
     * distributed under the License is distributed on an &quot;AS IS&quot; BASIS,
     * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
     * See the License for the specific language governing permissions and
     * limitations under the License.
     */</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">package</span> <span style="color: #006699;">com.example.android.apis.view</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.app.ListActivity</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.content.Context</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.os.Bundle</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.view.LayoutInflater</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.view.View</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.view.ViewGroup</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.widget.BaseAdapter</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.widget.TextView</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.widget.ImageView</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.graphics.BitmapFactory</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">android.graphics.Bitmap</span><span style="color: #339933;">;</span>
    <span style="color: #000000; font-weight: bold;">import</span> <span style="color: #006699;">com.example.android.apis.R</span><span style="color: #339933;">;</span>
    &nbsp;
    <span style="color: #008000; font-style: italic; font-weight: bold;">/**
     * Demonstrates how to write an efficient list adapter. The adapter used in this example binds
     * to an ImageView and to a TextView for each row in the list.
     *
     * To work efficiently the adapter implemented here uses two techniques:
     * - It reuses the convertView passed to getView() to avoid inflating View when it is not necessary
     * - It uses the ViewHolder pattern to avoid calling findViewById() when it is not necessary
     *
     * The ViewHolder pattern consists in storing a data structure in the tag of the view returned by
     * getView(). This data structures contains references to the views we want to bind data to, thus
     * avoiding calls to findViewById() every time getView() is invoked.
     */</span>
    <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000000; font-weight: bold;">class</span> List14 <span style="color: #000000; font-weight: bold;">extends</span> ListActivity <span style="color: #009900;">&#123;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">class</span> EfficientAdapter <span style="color: #000000; font-weight: bold;">extends</span> BaseAdapter <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">private</span> LayoutInflater mInflater<span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">private</span> Bitmap mIcon1<span style="color: #339933;">;</span>
            <span style="color: #000000; font-weight: bold;">private</span> Bitmap mIcon2<span style="color: #339933;">;</span>
    &nbsp;
            <span style="color: #000000; font-weight: bold;">public</span> EfficientAdapter<span style="color: #009900;">&#40;</span><span style="color: #003399;">Context</span> context<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #666666; font-style: italic;">// Cache the LayoutInflate to avoid asking for a new one each time.</span>
                mInflater <span style="color: #339933;">=</span> LayoutInflater.<span style="color: #006633;">from</span><span style="color: #009900;">&#40;</span>context<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
                <span style="color: #666666; font-style: italic;">// Icons bound to the rows.</span>
                mIcon1 <span style="color: #339933;">=</span> BitmapFactory.<span style="color: #006633;">decodeResource</span><span style="color: #009900;">&#40;</span>context.<span style="color: #006633;">getResources</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, R.<span style="color: #006633;">drawable</span>.<span style="color: #006633;">icon48x48_1</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                mIcon2 <span style="color: #339933;">=</span> BitmapFactory.<span style="color: #006633;">decodeResource</span><span style="color: #009900;">&#40;</span>context.<span style="color: #006633;">getResources</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span>, R.<span style="color: #006633;">drawable</span>.<span style="color: #006633;">icon48x48_2</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            <span style="color: #008000; font-style: italic; font-weight: bold;">/**
             * The number of items in the list is determined by the number of speeches
             * in our array.
             *
             * @see android.widget.ListAdapter#getCount()
             */</span>
            <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">int</span> getCount<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #000000; font-weight: bold;">return</span> DATA.<span style="color: #006633;">length</span><span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            <span style="color: #008000; font-style: italic; font-weight: bold;">/**
             * Since the data comes from an array, just returning the index is
             * sufficent to get at the data. If we were using a more complex data
             * structure, we would return whatever object represents one row in the
             * list.
             *
             * @see android.widget.ListAdapter#getItem(int)
             */</span>
            <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">Object</span> getItem<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> position<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #000000; font-weight: bold;">return</span> position<span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            <span style="color: #008000; font-style: italic; font-weight: bold;">/**
             * Use the array index as a unique id.
             *
             * @see android.widget.ListAdapter#getItemId(int)
             */</span>
            <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">long</span> getItemId<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> position<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #000000; font-weight: bold;">return</span> position<span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            <span style="color: #008000; font-style: italic; font-weight: bold;">/**
             * Make a view to hold each row.
             *
             * @see android.widget.ListAdapter#getView(int, android.view.View,
             *      android.view.ViewGroup)
             */</span>
            <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #003399;">View</span> getView<span style="color: #009900;">&#40;</span><span style="color: #000066; font-weight: bold;">int</span> position, <span style="color: #003399;">View</span> convertView, ViewGroup parent<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                <span style="color: #666666; font-style: italic;">// A ViewHolder keeps references to children views to avoid unneccessary calls</span>
                <span style="color: #666666; font-style: italic;">// to findViewById() on each row.</span>
                ViewHolder holder<span style="color: #339933;">;</span>
    &nbsp;
                <span style="color: #666666; font-style: italic;">// When convertView is not null, we can reuse it directly, there is no need</span>
                <span style="color: #666666; font-style: italic;">// to reinflate it. We only inflate a new View when the convertView supplied</span>
                <span style="color: #666666; font-style: italic;">// by ListView is null.</span>
                <span style="color: #000000; font-weight: bold;">if</span> <span style="color: #009900;">&#40;</span>convertView <span style="color: #339933;">==</span> <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
                    convertView <span style="color: #339933;">=</span> mInflater.<span style="color: #006633;">inflate</span><span style="color: #009900;">&#40;</span>R.<span style="color: #006633;">layout</span>.<span style="color: #006633;">list_item_icon_text</span>, <span style="color: #000066; font-weight: bold;">null</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
                    <span style="color: #666666; font-style: italic;">// Creates a ViewHolder and store references to the two children views</span>
                    <span style="color: #666666; font-style: italic;">// we want to bind data to.</span>
                    holder <span style="color: #339933;">=</span> <span style="color: #000000; font-weight: bold;">new</span> ViewHolder<span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    holder.<span style="color: #006633;">text</span> <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>TextView<span style="color: #009900;">&#41;</span> convertView.<span style="color: #006633;">findViewById</span><span style="color: #009900;">&#40;</span>R.<span style="color: #006633;">id</span>.<span style="color: #006633;">text</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                    holder.<span style="color: #006633;">icon</span> <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>ImageView<span style="color: #009900;">&#41;</span> convertView.<span style="color: #006633;">findViewById</span><span style="color: #009900;">&#40;</span>R.<span style="color: #006633;">id</span>.<span style="color: #006633;">icon</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
                    convertView.<span style="color: #006633;">setTag</span><span style="color: #009900;">&#40;</span>holder<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span> <span style="color: #000000; font-weight: bold;">else</span> <span style="color: #009900;">&#123;</span>
                    <span style="color: #666666; font-style: italic;">// Get the ViewHolder back to get fast access to the TextView</span>
                    <span style="color: #666666; font-style: italic;">// and the ImageView.</span>
                    holder <span style="color: #339933;">=</span> <span style="color: #009900;">&#40;</span>ViewHolder<span style="color: #009900;">&#41;</span> convertView.<span style="color: #006633;">getTag</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                <span style="color: #009900;">&#125;</span>
    &nbsp;
                <span style="color: #666666; font-style: italic;">// Bind the data efficiently with the holder.</span>
                holder.<span style="color: #006633;">text</span>.<span style="color: #006633;">setText</span><span style="color: #009900;">&#40;</span>DATA<span style="color: #009900;">&#91;</span>position<span style="color: #009900;">&#93;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
                holder.<span style="color: #006633;">icon</span>.<span style="color: #006633;">setImageBitmap</span><span style="color: #009900;">&#40;</span><span style="color: #009900;">&#40;</span>position <span style="color: #339933;">&amp;</span> <span style="color: #cc66cc;">1</span><span style="color: #009900;">&#41;</span> <span style="color: #339933;">==</span> <span style="color: #cc66cc;">1</span> <span style="color: #339933;">?</span> mIcon1 <span style="color: #339933;">:</span> mIcon2<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
    &nbsp;
                <span style="color: #000000; font-weight: bold;">return</span> convertView<span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
    &nbsp;
            <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">class</span> ViewHolder <span style="color: #009900;">&#123;</span>
                TextView text<span style="color: #339933;">;</span>
                ImageView icon<span style="color: #339933;">;</span>
            <span style="color: #009900;">&#125;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        @Override
        <span style="color: #000000; font-weight: bold;">public</span> <span style="color: #000066; font-weight: bold;">void</span> onCreate<span style="color: #009900;">&#40;</span>Bundle savedInstanceState<span style="color: #009900;">&#41;</span> <span style="color: #009900;">&#123;</span>
            <span style="color: #000000; font-weight: bold;">super</span>.<span style="color: #006633;">onCreate</span><span style="color: #009900;">&#40;</span>savedInstanceState<span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
            setListAdapter<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">new</span> EfficientAdapter<span style="color: #009900;">&#40;</span><span style="color: #000000; font-weight: bold;">this</span><span style="color: #009900;">&#41;</span><span style="color: #009900;">&#41;</span><span style="color: #339933;">;</span>
        <span style="color: #009900;">&#125;</span>
    &nbsp;
        <span style="color: #000000; font-weight: bold;">private</span> <span style="color: #000000; font-weight: bold;">static</span> <span style="color: #000000; font-weight: bold;">final</span> <span style="color: #003399;">String</span><span style="color: #009900;">&#91;</span><span style="color: #009900;">&#93;</span> DATA <span style="color: #339933;">=</span> Cheeses.<span style="color: #006633;">sCheeseStrings</span><span style="color: #339933;">;</span>
    <span style="color: #009900;">&#125;</span></pre></td></tr></table><p class="theCode" style="display:none;">/*
     * Copyright (C) 2008 The Android Open Source Project
     *
     * Licensed under the Apache License, Version 2.0 (the &quot;License&quot;);
     * you may not use this file except in compliance with the License.
     * You may obtain a copy of the License at
     *
     *      http://www.apache.org/licenses/LICENSE-2.0
     *
     * Unless required by applicable law or agreed to in writing, software
     * distributed under the License is distributed on an &quot;AS IS&quot; BASIS,
     * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
     * See the License for the specific language governing permissions and
     * limitations under the License.
     */
    
    package com.example.android.apis.view;
    
    import android.app.ListActivity;
    import android.content.Context;
    import android.os.Bundle;
    import android.view.LayoutInflater;
    import android.view.View;
    import android.view.ViewGroup;
    import android.widget.BaseAdapter;
    import android.widget.TextView;
    import android.widget.ImageView;
    import android.graphics.BitmapFactory;
    import android.graphics.Bitmap;
    import com.example.android.apis.R;
    
    /**
     * Demonstrates how to write an efficient list adapter. The adapter used in this example binds
     * to an ImageView and to a TextView for each row in the list.
     *
     * To work efficiently the adapter implemented here uses two techniques:
     * - It reuses the convertView passed to getView() to avoid inflating View when it is not necessary
     * - It uses the ViewHolder pattern to avoid calling findViewById() when it is not necessary
     *
     * The ViewHolder pattern consists in storing a data structure in the tag of the view returned by
     * getView(). This data structures contains references to the views we want to bind data to, thus
     * avoiding calls to findViewById() every time getView() is invoked.
     */
    public class List14 extends ListActivity {
    
        private static class EfficientAdapter extends BaseAdapter {
            private LayoutInflater mInflater;
            private Bitmap mIcon1;
            private Bitmap mIcon2;
    
            public EfficientAdapter(Context context) {
                // Cache the LayoutInflate to avoid asking for a new one each time.
                mInflater = LayoutInflater.from(context);
    
                // Icons bound to the rows.
                mIcon1 = BitmapFactory.decodeResource(context.getResources(), R.drawable.icon48x48_1);
                mIcon2 = BitmapFactory.decodeResource(context.getResources(), R.drawable.icon48x48_2);
            }
    
            /**
             * The number of items in the list is determined by the number of speeches
             * in our array.
             *
             * @see android.widget.ListAdapter#getCount()
             */
            public int getCount() {
                return DATA.length;
            }
    
            /**
             * Since the data comes from an array, just returning the index is
             * sufficent to get at the data. If we were using a more complex data
             * structure, we would return whatever object represents one row in the
             * list.
             *
             * @see android.widget.ListAdapter#getItem(int)
             */
            public Object getItem(int position) {
                return position;
            }
    
            /**
             * Use the array index as a unique id.
             *
             * @see android.widget.ListAdapter#getItemId(int)
             */
            public long getItemId(int position) {
                return position;
            }
    
            /**
             * Make a view to hold each row.
             *
             * @see android.widget.ListAdapter#getView(int, android.view.View,
             *      android.view.ViewGroup)
             */
            public View getView(int position, View convertView, ViewGroup parent) {
                // A ViewHolder keeps references to children views to avoid unneccessary calls
                // to findViewById() on each row.
                ViewHolder holder;
    
                // When convertView is not null, we can reuse it directly, there is no need
                // to reinflate it. We only inflate a new View when the convertView supplied
                // by ListView is null.
                if (convertView == null) {
                    convertView = mInflater.inflate(R.layout.list_item_icon_text, null);
    
                    // Creates a ViewHolder and store references to the two children views
                    // we want to bind data to.
                    holder = new ViewHolder();
                    holder.text = (TextView) convertView.findViewById(R.id.text);
                    holder.icon = (ImageView) convertView.findViewById(R.id.icon);
    
                    convertView.setTag(holder);
                } else {
                    // Get the ViewHolder back to get fast access to the TextView
                    // and the ImageView.
                    holder = (ViewHolder) convertView.getTag();
                }
    
                // Bind the data efficiently with the holder.
                holder.text.setText(DATA[position]);
                holder.icon.setImageBitmap((position &amp; 1) == 1 ? mIcon1 : mIcon2);
    
                return convertView;
            }
    
            static class ViewHolder {
                TextView text;
                ImageView icon;
            }
        }
    
        @Override
        public void onCreate(Bundle savedInstanceState) {
            super.onCreate(savedInstanceState);
            setListAdapter(new EfficientAdapter(this));
        }
    
        private static final String[] DATA = Cheeses.sCheeseStrings;
    }</p></div>
    ";}
categories:
  - Android
tags:
  - Adapter
  - ViewHolder

---
这个ViewHolder到底是什么呢？我们可以在官方sample看到这段代码  
<a href="http://developer.android.com/resources/samples/ApiDemos/src/com/example/android/apis/view/List14.html" title="http://developer.android.com/resources/samples/ApiDemos/src/com/example/android/apis/view/List14.html" target="_blank">http://developer.android.com/resources/samples/ApiDemos/src/com/example/android/apis/view/List14.html</a>
<pre escaped="true" lang="java">static class ViewHolder {
            TextView text;
            ImageView icon;
        }</pre>
可以看到它只是一个静态类，**它的作用就在于减少不必要的调用findViewById**  
完整的官方例子，官方例子中convertView 也是避免inflating View。  
然后把对底下的控件引用存在ViewHolder里面，再在View.setTag(holder)把它放在view里，下次就可以直接取了。
效率相差多少？看这篇文章：<a href="http://www.ideasandroid.com/archives/295#more-295" title="http://www.ideasandroid.com/archives/295#more-295" target="_blank">Android开发之ListView 适配器（Adapter）优化</a>
<pre escaped="true" lang="java">/*
 * Copyright (C) 2008 The Android Open Source Project
 *
 * Licensed under the Apache License, Version 2.0 (the "License");
 * you may not use this file except in compliance with the License.
 * You may obtain a copy of the License at
 *
 *      http://www.apache.org/licenses/LICENSE-2.0
 *
 * Unless required by applicable law or agreed to in writing, software
 * distributed under the License is distributed on an "AS IS" BASIS,
 * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
 * See the License for the specific language governing permissions and
 * limitations under the License.
 */

package com.example.android.apis.view;

import android.app.ListActivity;
import android.content.Context;
import android.os.Bundle;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;
import android.widget.BaseAdapter;
import android.widget.TextView;
import android.widget.ImageView;
import android.graphics.BitmapFactory;
import android.graphics.Bitmap;
import com.example.android.apis.R;

/**
 * Demonstrates how to write an efficient list adapter. The adapter used in this example binds
 * to an ImageView and to a TextView for each row in the list.
 *
 * To work efficiently the adapter implemented here uses two techniques:
 * - It reuses the convertView passed to getView() to avoid inflating View when it is not necessary
 * - It uses the ViewHolder pattern to avoid calling findViewById() when it is not necessary
 *
 * The ViewHolder pattern consists in storing a data structure in the tag of the view returned by
 * getView(). This data structures contains references to the views we want to bind data to, thus
 * avoiding calls to findViewById() every time getView() is invoked.
 */
public class List14 extends ListActivity {

    private static class EfficientAdapter extends BaseAdapter {
        private LayoutInflater mInflater;
        private Bitmap mIcon1;
        private Bitmap mIcon2;

        public EfficientAdapter(Context context) {
            // Cache the LayoutInflate to avoid asking for a new one each time.
            mInflater = LayoutInflater.from(context);

            // Icons bound to the rows.
            mIcon1 = BitmapFactory.decodeResource(context.getResources(), R.drawable.icon48x48_1);
            mIcon2 = BitmapFactory.decodeResource(context.getResources(), R.drawable.icon48x48_2);
        }

        /**
         * The number of items in the list is determined by the number of speeches
         * in our array.
         *
         * @see android.widget.ListAdapter#getCount()
         */
        public int getCount() {
            return DATA.length;
        }

        /**
         * Since the data comes from an array, just returning the index is
         * sufficent to get at the data. If we were using a more complex data
         * structure, we would return whatever object represents one row in the
         * list.
         *
         * @see android.widget.ListAdapter#getItem(int)
         */
        public Object getItem(int position) {
            return position;
        }

        /**
         * Use the array index as a unique id.
         *
         * @see android.widget.ListAdapter#getItemId(int)
         */
        public long getItemId(int position) {
            return position;
        }

        /**
         * Make a view to hold each row.
         *
         * @see android.widget.ListAdapter#getView(int, android.view.View,
         *      android.view.ViewGroup)
         */
        public View getView(int position, View convertView, ViewGroup parent) {
            // A ViewHolder keeps references to children views to avoid unneccessary calls
            // to findViewById() on each row.
            ViewHolder holder;

            // When convertView is not null, we can reuse it directly, there is no need
            // to reinflate it. We only inflate a new View when the convertView supplied
            // by ListView is null.
            if (convertView == null) {
                convertView = mInflater.inflate(R.layout.list_item_icon_text, null);

                // Creates a ViewHolder and store references to the two children views
                // we want to bind data to.
                holder = new ViewHolder();
                holder.text = (TextView) convertView.findViewById(R.id.text);
                holder.icon = (ImageView) convertView.findViewById(R.id.icon);

                convertView.setTag(holder);
            } else {
                // Get the ViewHolder back to get fast access to the TextView
                // and the ImageView.
                holder = (ViewHolder) convertView.getTag();
            }

            // Bind the data efficiently with the holder.
            holder.text.setText(DATA[position]);
            holder.icon.setImageBitmap((position & 1) == 1 ? mIcon1 : mIcon2);

            return convertView;
        }

        static class ViewHolder {
            TextView text;
            ImageView icon;
        }
    }

    @Override
    public void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setListAdapter(new EfficientAdapter(this));
    }

    private static final String[] DATA = Cheeses.sCheeseStrings;
}</pre>