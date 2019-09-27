# crmenu
creando menus
diseño
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    xmlns:app="http://schemas.android.com/apk/res-auto"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical">

    <FrameLayout
        android:layout_width="match_parent"
        android:layout_height="0dp"
        android:layout_weight="1">

        <com.mikhaellopez.circularimageview.CircularImageView
            android:id="@+id/circularImageView"
            android:layout_width="300dp"
            android:layout_height="300dp"
            android:layout_gravity="center"
            android:src="@drawable/logo"
            app:civ_border="true"
            app:civ_border_color="#3f51b5"
            app:civ_border_width="8dp"
            app:civ_shadow="true"
            app:civ_shadow_color="#3f51b5"
            app:civ_shadow_radius="10" />

    </FrameLayout>

    <LinearLayout
        android:layout_width="240dp"
        android:layout_height="wrap_content"
        android:layout_marginBottom="40dp"
        android:gravity="center"
        android:orientation="vertical">

        <SeekBar
            android:id="@+id/seekBarBorderWidth"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:max="40"
            android:progress="8" />

        <SeekBar
            android:id="@+id/seekBarShadowRadius"
            android:layout_width="match_parent"
            android:layout_height="wrap_content"
            android:layout_marginTop="10dp"
            android:max="40"
            android:progress="8" />

        <com.larswerkman.lobsterpicker.sliders.LobsterShadeSlider
            android:id="@+id/shadeSlider"
            android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:layout_marginTop="10dp" />

    </LinearLayout>

</LinearLayout>
codificacion
package com.mikhaellopez.circularimageviewsample

import android.os.Bundle
import android.widget.SeekBar
import androidx.appcompat.app.AppCompatActivity
import com.larswerkman.lobsterpicker.OnColorListener
import com.larswerkman.lobsterpicker.sliders.LobsterShadeSlider
import kotlinx.android.synthetic.main.activity_main.*

class MainActivity : AppCompatActivity() {

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)

        seekBarBorderWidth.onProgressChanged { circularImageView.borderWidth = it.toFloat() * resources.displayMetrics.density.toInt() }
        seekBarShadowRadius.onProgressChanged { circularImageView.shadowRadius = it.toFloat() }
        shadeSlider.onColorChanged {
            circularImageView.borderColor = it
            circularImageView.shadowColor = it
        }
    }

    //region Extensions
    private fun SeekBar.onProgressChanged(onProgressChanged: (Int) -> Unit) {
        setOnSeekBarChangeListener(object : SeekBar.OnSeekBarChangeListener {
            override fun onProgressChanged(seekBar: SeekBar?, progress: Int, fromUser: Boolean) {
                onProgressChanged(progress)
            }

            override fun onStartTrackingTouch(seekBar: SeekBar?) {
                // Nothing
            }

            override fun onStopTrackingTouch(seekBar: SeekBar?) {
                // Nothing
            }
        })
    }

    private fun LobsterShadeSlider.onColorChanged(onColorChanged: (Int) -> Unit) {
        addOnColorListener(object : OnColorListener {
            override fun onColorChanged(color: Int) {
                onColorChanged(color)
            }

            override fun onColorSelected(color: Int) {
                // Nothing
            }
        })
    }
    //endregion

}
